---
layout: post
title: "The History of Computing, Part III: German Engineering, and Moving Computers"
---

# Wartime Effort, from the Other Side
Most people, when they think about WWII, don't think about the German perspective, and when they do, it's usually considered from the point of view of "evil enemy nation who did some stuff." Today, I shall consider quite a different side to the German war effort - the technological advances that came from it, specifically within the realm of computation. Of course, this is a vast topic, so only a small part of it shall be considered in this post.

Mechanical computing was used a lot during WWII, and in the years leading up to it, predominantly by the military, on both sides, though academic applications were also quite prevelant. One man was particularly famous for his mechanical, and elecctromechanical, machines. This was Konrad Zuse, a serial computer engineer who invented many such machines.

The first, the Z1, at the time known as the V1, was developed and built between 1935 and 1938. Renamed to differentiate it from a weapon used during the same time period, and destroyed during a bombing run on Berlin in 1943, the Z1 was the first of its kind, in many respects - it significantly expanded the capabilities of computers at the time. The computer used binary to represent numbers, and calculated using Boolean logic (operations on the 1s and 0s), simplifying computation and storage significantly.

Additionally, the computer could represent and calculate with real numbers (decimal numbers, as opposed to just whole numbers), allowing the machine to be far more effective at scientific computation. No other computation device in the world so far had these features.

Alas, the Z1 was not reliable in operation. It relied almost exclusively on metal strips, rods, and other such mechanical parts to represent the individual values and computational elements, which would regularly stick, as the parts were often not synchronised with one another. In a classic display of Silicon Valley culture, many years before Silicon Valley was even dreamt of, Zuse constructed the Z1 in his parents' apartment, using funding from friends and family to do so.

Later, Zuse built upon the Z1, replacing the arithmetic and control machinery (which we'd now refer to as a CPU or a processor) with relays taken from telephone exchange equipment. This vastly improved the reliability of the machine, now dubbed the Z2. This work was based on the work, and advice, of Helmut Schreyer, who while studying for a Doctorate at the Berlin Institute of Technology in 1937, worked on memory built from Boolean logic.

Schreyer then worked with Zuse to build further upon the design, arriving at the Z3 machine. Composed entirely of relays, the Z3 was designed for use by the German Laboratory for Aviation, as part of the war effort, where it was used in research on flutter, a problem in aerodynamics and therefore in aircraft design. For this reason, the machine was kept very secret by the Reich.

The Z3 is notable for more than just its political position, however. It added exception values to its computation, as well as +/- infinity, and undefined. This meant that any errors during a calculation could be passed through the calculation, and rather than giving a random value at the end, clearly presented as an error. The easiest example to point to would be if the machine attempted to divide by 0.

Additionally, the Z3 is considered the first machine to be Turing complete. The technical definition of Turing completeness isn't too important here, however this was a major milestone - what it effectively means is that the Z3 was the first general purpose computer. It could be used to perform any calculation, as opposed to fixed equations. The way it did this was unorthadox, and is no longer used, requiring every possible calculation to be done and the unneeded ones discarded, however it was possible nontheless.

# Zuse KG, the Z4, and Plankalkül
The Z4 was an expansion of the Z3, once again, simplifying it significantly in places and adding new capabilities, such as abstract references (data could now be named, as opposed to needing to recall its location manually), several instructions such as trigonometric functions and square roots, and the ability to start running a different piece of code, and return later, a technique known as subroutines. It also added the ability to change which instructions were run based on some condition (if this do that, otherwise do something else).

More notably, however, the Z4 was the words first commercial digital computer. Originally, as with the Z3, it was intended for use by the German war effort, however the construction of the original machine was completed days before the war ended. In February 1945, to prevent the machine falling into Soviet hands, the Z4 was moved from Berlin, and relocated to Goettingen, where it was completed (and later, moved again to Hinterstein for the same reason).

Zuse founded Zuse KG in 1949, a company through which the Z4 was commercialised. The first customer was ETH Zurich, who operated the machine from 1950-1954. For a while, the Z4 was the only digital computer in continental Europe.

After selling the Z4, Zuse KG then went on to sell several more machines, of several different designs - the Z5, the Z11, and the Z22. Each added new capabilities to the machine, such as new instructions,new devices, and new technologies such as vacuum tubes.

Zuse, and Zuse KG, aren't notable solely for the Z-series of computers, however. In 1942, Zuse developed Plankalkül, one of the first programming languages, for use on his computers. This work was not published for a long time, due to the effects of the war, however Zuse continued to work nontheless, working on a chess program, and a book about the language, which was never published. The language is remarkably different to nearly every other programming language, and has been compared to APL. It draws a significant amount of inspiration from mathematical notation, and builds upon it, generalising it in the process.

Also visible at [EsseX-Files](https://essexfiles.blogspot.co.uk/2017/12/the-history-of-computing-part-iii.html)