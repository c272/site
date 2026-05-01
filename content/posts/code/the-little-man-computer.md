---
layout: post
title: The Little Man Computer
date: 2018-03-29
tags:
  - NodeJS
description: >
  Emulation for dummies.
coverImage: /img/covers/littlemancomputer.png
url: /blog/code/the-little-man-computer/
---

Over the past couple of months, apart from writing my book, “You Suck at Programming” [^1], I’ve been working on an emulator/interpreter for the famous computer simulation “Little Man Computer", by Peter Higginson. It was created many years ago to help students learn about how the CPU and memory worked and interacted with each other, and was a great way for me to try and understand some lower level emulation, as it has an instruction set consisting of just nine operations. These operations are:

~~~
ADD – Addition
SUB – Subtraction
DAT – Data Storage
LDA – Load Data
STA – Store Data
HLT – Halt Program
BIZ – Branch if Zero
BRA – Branch Always
BZP – Branch if Zero or Positive
~~~

They all sounded fairly simple to implement, so I went about creating the first prototypes for the interpreter of this program. Initially, I tried to create a dictionary with 99 data spaces to store my data, however this ended up causing a lot of problems for me down the line. I eventually had to scrap the entire idea, and ended up just using a simple two dimensional array. Now that that was sorted, I needed to somehow get a standard data format including data and addresses, and have an interpreter read them properly. Luckily, Little Man Computer is close enough to a real computer that it uses “opcodes”, small (in this case 3 character) strings which tell you which command is being executed, and at what address. So, the format I came up with looked like this:

~~~
[[00, 901], [01, 105], [02, 902]]
~~~

The 2D array contains in the first position the address of the current memory slot (ascending from 00), and in the second position the opcode of the command. “901” is input, and “902” output, with “1” being addition, and “5” being the address that is added to the accumulator’s current value (which is what the ADD command actually does, but more on the accumulator later). So, by that definition, this program just takes an input, adds the value of address 5 to it, and spits out the answer.

I then realised that I needed some way of storing the value of the accumulator, program counter, and all the other registers within the LMC CPU. So, I just used basic integers. Simple.

The interpreter I wrote has a chain of decoding that it has to complete before it reaches the “execution” part of “fetch, decode, execute”. The fetching has already been done in the form of the two dimensional array, and the decoding is the fun bit. The interpreter loops through each value in the array, checking the memory slot’s second position for the opcode, and one by one executing the commands. If a branch is found to be true, then the interpreter loops through all positions in the two dimensional array until the first position’s value matches the last two characters of the branch (like 804, which would search for address “04” if the value was positive or zero). The code will then continue from that location until a halting operation (HLT).

For this, however, I had to create an essentially entirely new file format called “Little Man Script, or .LMS. I’ve included a compiler in the project that allows you to convert plaintext commands (like “LDA 04” or “STA 99”) into a formatted “.LMS” file which you can run with either the executable file or the raw Javascript.

To see this in action for yourself, and to try writing an assembly script on your own (you can use the provided compiler to convert text files) navigate to my GitHub page by clicking [here](https://github.com/c272/jLMC), and downloading a zip of all the files in the source.

That’s all for now, but I’ll catch up with you soon when the book is nearer to release.

[^1]: This book was later renamed to "Programming at Light Speed".
