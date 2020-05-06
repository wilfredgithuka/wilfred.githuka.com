---
title: "8bit Home - Building an 8-bit computer from scratch"
date: 2020-01-16T08:47:51+03:00
draft: false
---
Building a computer from scratch is a crazy idea, given the small details
one has to be careful with. Also the time investment for debugging is immense.

But the learning content is incredible.

This is the reason why am starting this long journey of building an 8bit computer
from scratch. Am building mine from TTL chips using the kits provided by
[Ben Easter](https://eater.net/8bit)

## What is an 8bit Computer?

In computing a bit is 0 and 1, therefore the following occurs:

* 1 bit is 0 and 1.
* 2 bits = 4 0s and 1s
* 4 bits = 8 possible states of 0s and 1s
* 8 bits = 256 possible states of 0s and 1s

There are 28 (256) different possible values for 8 bits. When unsigned, it has possible values ranging from 0 to 255; when signed, it has -128 to 127. 

8-bit integers, memory addresses, or other data units are those that are 8 bits (1 octet) wide. Also, 8-bit CPU and ALU architectures are those that are based on registers, address buses, or data buses of that size. 8-bit is also a generation of microcomputers in which 8-bit microprocessors were the norm.


Someting to note: Most 8-bit operations can only be performed on the 8-bit accumulator (the A register). For 8-bit operations with two operands, the other operand can be either an immediate value, another 8-bit register, or a memory byte addressed by the 16-bit register pair HL. Direct copying is supported between any two 8-bit registers and between any 8-bit register and an HL-addressed memory byte. Due to the regular encoding of the MOV instruction (using a quarter of available opcode space), there are redundant codes to copy a register into itself (MOV B,B, for instance), which are of little use, except for delays. However, what would have been a copy from the HL-addressed cell into itself (i.e., MOV M,M) is instead used to encode the halt (HLT) instruction, halting execution until an external reset or interrupt occurs. 

## The Kit

![kit](https://cdn.shopify.com/s/files/1/0089/0647/3536/products/computer-hero-42_550x825.png?v=1544158524)

The Complete Kit bundle retails at USD 269(Ksh.30,000).

This set of 4 kits, along with series of videos on YouTube will help you develop a deep understanding of how programmable CPUs really work.

This bundle includes:

* Clock module
* Registers and ALU
* RAM and program counter
* Output and control logic

See the descriptions for each kit for a complete list of parts included.

Note: Each kit includes schematic diagrams, but full assembly instructions are only provided through the YouTube videos. The kits include pointers to which videos to follow along with.

I bought my kit bundle and it took 3 weeks to arrive. Upon reaching the JKIA Airport there were some custom charges which came to about KES 16,000. I wouldn't recommend
this method, it waaaay too expensive. 

## The Project Index

 1. Clock Module
    * [555 Clock Signal Basics](https://wilfred.githuka.com/post/555/) 
    * [Monostable](https://wilfred.githuka.com/post/monostable/)
    * [Bistable](https://wilfred.githuka.com/post/bistable)
 2. Arithmetic Logic Unit
 3. Random Access Memory(RAM) module
 4. Program Counter
 5. Output Register
 6. Bringing It All Together
 7. CPU Control Logic
