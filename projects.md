---
layout: default
title: Projects
navigable: true
---
# Software
## [Redox OS](https://redox-os.org)
Redox is a microkernel-based operating system written in Rust. I am currently involved in a lot of ACPI work, specifically developing an AML interpreter for use within the kernel, and to develop a driver for the High Precision Event Timer (HPET), as defined in a document referenced by the ACPI specification.

AML is a bytecode in the ACPI specification, which contains a lot of important details on how the machine runs - it contains certain values needed to power the machine down, for example, and control methods for operating a lot of the machine hardware. This needs to be parsed, and then intercepted, to achieve a lot of important administration tasks, and due to the design of the spec, a recursive descent, multi-pass parser is required, in kernel mode.

## LLProt
As it is in its early stages still, LLProt is yet to be released as open source. LLProt is a DSL, for specifying the underlying structure of network protocols. It is similar to ProtoBuf, however with the constraint that bit- and byte-level fidelity is required, to ensure interoperability with existing protocols.

## [DDMP](https://github.com/CWood1/DDMP)
Distributed DHCP Management Protocol - a protocol layer to sit on top of DHCP, in order to facilitate the allocation of addresses from multiple servers, from the same address pool. Development focuses primarily around mesh networks, however project may be useful in other contexts, such as data centres.

## [Patient Panic](https://github.com/CWood1/chimed)
A project completed as part of a team, for a competition while at university. I did the bulk of the programming, though the design itself was not mine. The intention behind the competition, and the design space we were operating in, was to design a game to call attention to blame culture, and to prompt people to think deeper about the assumptions they make.

# Languages
I am currently working on learning Mandarin Chinese, though I am currently only at beginner level. Other languages I have an interest in, though am yet to begin learning, are:

 - Greek
 - Esperanto
 - Arabic
 - Tamil
 - German
 - Russian
 - Korean
 - Japanese
 - Spanish