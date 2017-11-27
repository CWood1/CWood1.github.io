---
layout: post
title: "Memory Profiling for Low Level Engineering: Massif"
---

Memory profiling for high level work is pretty easy - often, the language runtime is perfectly capable of doing it for you, providing reports and pretty graphs as you desire. When you get into lower level programming, however, we lose this. How do we get around this problem?

# Massif
If you're like me, you probably thought for a long time that Valgrind was a leak checking tool and that was it. That's one thing it can do, yes, but it can do a lot more as well - it's not a tool, it's a suite of them. Memory profiling is one.

Massif is designed to measure memory usage in detail. By default it measures the heap, just about every aspect of it, and can be made to look at the stack as well. Thus, we can see where to optimise memory usage, and also detect memory "leaks" in which we forget to free, but don't actually lose track of the block (leak-check cannot do this).

Needless to say, this is a pretty important thing to be able to do for any code that isn't throwaway - we don't want our programs to consume silly amounts of memory in a hot inner loop when we can optimise it, and we don't want to have a bunch of memory sitting around until the kernel shouts at us for wasting so much of it. Neither of those give the impression of quality when end users get hold of your code, and the ops team won't be very happy about writing scripts and provisioning extra boxes to handle that either.

# First Forays into Profiling with Massif
Three important steps are needed to have Massif do anything useful. The first is to build your software with debugging symbols in place. This varies per compiler and per language, but for C and C++, is achieved using the `-g` flag.

The next thing to do is to run the software using Massif, and exercise the parts of it you have an interest in profiling. This is done using the command, `valgrind --tool=massif myprog`. This will output a file called massif.out.<pid>, containing the memory profiling data.

Lastly, `ms_print <file>` gives us the two key pieces of information needed to perform the profiling.

## Memory Usage Graphs
The graph produced will look something like this:
```
19.63^                                               ###                      
     |                                               #                        
     |                                               #  ::                    
     |                                               #  : :::                 
     |                                      :::::::::#  : :  ::               
     |                                      :        #  : :  : ::             
     |                                      :        #  : :  : : :::          
     |                                      :        #  : :  : : :  ::        
     |                            :::::::::::        #  : :  : : :  : :::     
     |                            :         :        #  : :  : : :  : :  ::   
     |                        :::::         :        #  : :  : : :  : :  : :: 
     |                     @@@:   :         :        #  : :  : : :  : :  : : @
     |                   ::@  :   :         :        #  : :  : : :  : :  : : @
     |                :::: @  :   :         :        #  : :  : : :  : :  : : @
     |              :::  : @  :   :         :        #  : :  : : :  : :  : : @
     |            ::: :  : @  :   :         :        #  : :  : : :  : :  : : @
     |         :::: : :  : @  :   :         :        #  : :  : : :  : :  : : @
     |       :::  : : :  : @  :   :         :        #  : :  : : :  : :  : : @
     |    :::: :  : : :  : @  :   :         :        #  : :  : : :  : :  : : @
     |  :::  : :  : : :  : @  :   :         :        #  : :  : : :  : :  : : @
   0 +----------------------------------------------------------------------->KB     0                                                                   29.48

Number of snapshots: 25
 Detailed snapshots: [9, 14 (peak), 24]
```
(borrowed from the Valgrind documentation).

Sometimes we may need the parameter `--time-unit=B` passed to `ms_print` - by default, it times in terms of executed instructions, which may not be the best measure, especially for short, or uninterractive, programs.

What we have, thus, is a histogram, allowing us to see the exact memory profile as it changed over time. This lets us see at a glance if anything stands out, such as slowly growing memory or huge spikes. What counts as standing out depends on the software under test, and how you drive it during testing, so human judgement is needed here.

## Detailed Usage Reports
The detailed report, following the graph, will look similar to this (again taken from Valgrind's documentation for ease):
```
--------------------------------------------------------------------------------
  n        time(B)         total(B)   useful-heap(B) extra-heap(B)    stacks(B)
--------------------------------------------------------------------------------
  0              0                0                0             0            0
  1          1,008            1,008            1,000             8            0
  2          2,016            2,016            2,000            16            0
  3          3,024            3,024            3,000            24            0
  4          4,032            4,032            4,000            32            0
  5          5,040            5,040            5,000            40            0
  6          6,048            6,048            6,000            48            0
  7          7,056            7,056            7,000            56            0
  8          8,064            8,064            8,000            64            0
  9          9,072            9,072            9,000            72            0
99.21% (9,000B) (heap allocation functions) malloc/new/new[], --alloc-fns, etc.
->99.21% (9,000B) 0x804841A: main (example.c:20)
 10         10,080           10,080           10,000            80            0
 11         12,088           12,088           12,000            88            0
 12         16,096           16,096           16,000            96            0
 13         20,104           20,104           20,000           104            0
 14         20,104           20,104           20,000           104            0
99.48% (20,000B) (heap allocation functions) malloc/new/new[], --alloc-fns, etc.
->49.74% (10,000B) 0x804841A: main (example.c:20)
| 
->39.79% (8,000B) 0x80483C2: g (example.c:5)
| ->19.90% (4,000B) 0x80483E2: f (example.c:11)
| | ->19.90% (4,000B) 0x8048431: main (example.c:23)
| |   
| ->19.90% (4,000B) 0x8048436: main (example.c:25)
|   
->09.95% (2,000B) 0x80483DA: f (example.c:10)
  ->09.95% (2,000B) 0x8048431: main (example.c:23)
 ```

Key things to note here are the time, and the running total, which match up to the graph from earlier. Heap overhead can also be seen, though it's rare this will be significant.

For allocation #9, a short description follows it, drilling down exactly how the memory was allocated (in this case, using a heap allocatoir such as malloc), and where it was allocated. The percentages are running totals for each allocaiton method/location.

Allocation #14 demonstrates this further along in the execution. In this case, we have a call tree to look at. Each tree root is a separate allocation location, and every branch leading to the root is, obviously, a different way to get to it (sometimes it won't be the specific allocation that needs optimising, just calling it less, so pay attention to this tree if you can).

If the call trees are particularly deep, we can pass `--depth=<n>` to Valgrind to see more detail. This often isn't needed, even when the call tree gets truncated, however occasionally it may harbor required detail.

# A Note on C++ (and probably other languages)
When I first started to use Massif, I used it on a C++ project I was working on, and the immediate thing I noted was an allocation far larger than anything else in the program, upfront in the ctors. This can be safely ignored, it's the runtime. Whenever you pull in headers like iostream, which allocate globals, they will appear in the graph.
