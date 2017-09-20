---
layout: post
title: "Project postmortem for AML"
---

Over summer, I did some work for [Redox](https://www.redox-os.org), to implement an interpreter for the ACPI Machine Language.

# Project Description
The Advanced Configuration and Power Interface, ACPI, is a specification developed to configure an operating system based on the hardware present in a computer, and to give it a way to control said hardware. As the name suggests, the primary job is to control power, though it contains provisions for many other jobs as well, such as thermal profiling and control, etc.

A large part of the specification, and the primary way this is achieved in recent versions of the specification, is to parse and interpret the Differentiated System Description Table, or DSDT, along with any Secondary System Description Tables, SSDTs. These tables contain AML bytecode, and by interpreting this bytecode, it is possible to build up a namespace of devices present, along with a list of methods to control them (and, in some cases, have the devices control the operating system as well, to save the operating system needing to poll devices for events).

My project was to implement an interpreter for AML, in the Redox kernel, and use it to parse the DSDT, and any SSDTs, in the correct order.

# The Architecture
Initially, I intended to parse the AML into a parse tree, which could then be interpreted, as is conventional wisdom. I continued with this plan for a significant amount of time into the project, and almost completed it before realising that after the initial parse, the entire tree would need to be executed to properly generate the namespace, which would result in a lot of duplicated code. Additionally, by executing in this manner, methods would need a different mechanism to execute, as the `execute` method would need to be recursive, resulting in more duplication.

The result was the need to rearchitecture the interpreter, to defy more conventional wisdom and run the bytecode as it's parsed. I could perhaps have used my initial architecture if I'd have had more experience implementing compilers/interpreters, however this was the first full interpreter I'd ever built. It is possible, as I gain more experience, I shall return to the AML interpreter and refactor/rearchitecture it again, cleaning it up.

# What Went Well?
The Redox community is incredibly supportive, and always quick to offer assistance where I needed it. Without them, this project wouldn't have been nearly as successful as it was.

Somewhere midway through the project, I realised my current architecture would cause a lot of lock contention with itself, as the namespace was protected by a mutex. Specifically, to find a method and call it, one would need to lock the namespace, preventing namespace modifications. Secondly, the AML interpreter sometimes needs to interact with other parts of the kernel, which in turn will sometimes need to call AML methods, creating a deadlock.

After a day or two of working out the logic of the locking mechanism, I discovered `RwLock` in Rust, implemented in the spin crate the kernel made use of. A small modification - cloning a method before calling it - meant this would solve both of my problems in one go, and significantly improve performance in the process. It is worth pointing out that just cloning methods would _technically_ achieve the same effect, however RwLock was my initial solution, and after modifying it with cloning, I decided to stick with it anyway for better performance.

Additionally, AML requires every loaded table to be marked with an index, known as a DDB Handle in the specification. For the tables in the root system descriptor table, the index is literally the index in the table, while for tables loaded in other ways (through AML, or through pointers in other tables), the index should increment for every table loaded. This resulted in a large part of the ACPI subsystem needing to be refactored, in order to support these indices. While admittedly tedious to rewrite a lot of code this way, the result was that a lot of dead code was eliminated, the subsystem was a lot more performant, and was also significantly neater. More refactoring is needed, however that fell outside the scope of this project.

# What Went Wrong?
For the initial work on the project, I began programming the interpreter using nom, a parser combinator framework for Rust. Sadly, I could not get it to compile for the kernel, so had to abandon it. This, however, turned out for the best later on, as nom would have been unable to properly parse method invocations due to the way the spec is written - MIs have no defined tag indicating what they are, rather using the method name, and also have nothing to indicate how many parameters are present. As it turns out, my architecture of parsing and executing simultaneously worked very effectively with these, as a full namespace was present to refer to, meaning multipass parsing was not needed.

Additionally, for a large part of the project, I was working from the 5.1 specification, errata A, only to find that 6.2 was out. Including erratas, this placed me an entire 9 versions behind the current. Thankfully, not a lot changed for AML, however a new opcode was added, meaning an interim pull request merged midway through the project broke Redox compatibility with Virtual Box for a while, before it was fixed by switching to the new spec.

# Conclusion
This project was, all in all, fantastic fun, and the most I've enjoyed programming in a while. I learned a significant amount during this project, including a broad overview of interpreters, as well as structuring code for concurrency/locking.

This was the largest project I've done to date, and it gave me a serious appreciation of both kernel programming, and for modern tools such as parser generators/parser combinator libraries. Now that I've had to create a fully fledged, recursive descent parser without one, I'll be avoiding not using them again at all costs, making sure I find a way to use such a tool to prevent all of the boilerplate I had to implement by hand this time around.

I'd do a few things differently from the outset next time, and intend to return to the Redox ACPI subsystem in future. My intention is, one day, to get Redox to ACPI 6.2 compatibility, however this is a much larger project, requiring a lot more time and effort. This shall be one of my next projects, however it must be balanced with other projects necessitated by university.
