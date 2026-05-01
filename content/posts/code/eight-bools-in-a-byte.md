---
layout: post
title: 8 Bools in a Byte
date: 2018-06-12
tags:
  - C++
description: >
  Efficiently packing booleans to save space I didn't need to.
coverImage: /img/covers/bitset.jpg
url: /blog/code/eight-bools-in-a-byte/
---

Storing booleans is an odd topic for the programming world, specifcally for storage. Typically, the smallest addressable chunk of memory is a byte, or 8 bits. The boolean type, having two states, requires just a single bit. This causes the following dilemma: If I want to store 8 bools, why am I using 8 bytes? That’s 64 bits, 56 more than I actually need to store that amount.

~~~cpp
//What a waste of storage!
bool option1 = true;
bool option2 = true;
bool option3 = true;
bool option4 = true;
bool option5 = true;
bool option6 = true;
bool option7 = true;
bool option8 = true;
~~~

C++, thankfully, has a way to fix this issue. Namely, through using 1 byte, with each individual bit in said byte being a boolean on it’s own. There are two methods to do this, one being much easier than the other, but I’ll explain both so that it becomes obvious what’s happening.

## The Manual Method
In C++, you can create 8 booleans in a byte by using Bitwise comparisons. So, let’s initialize some options.

~~~cpp
int optionOne = 0b0000'0001;
int optionTwo = 0b0000'0001;
int optionThree = 0b0000'0001;
int optionFour = 0b0000'0001;
int optionFive = 0b0000'0001;
int optionSix = 0b0000'0001;
int optionSeven = 0b0000'0001;
int optionEight = 0b0000'0001;
~~~

You may be thinking: “This takes up loads of storage, why would I use this instead of 8 booleans?”. Well, in terms of using a single set of 8, yes it does, however if you’re creating many instances of, for example, an enemy, which all have different possible status effects, this method is much more space-efficient than others. But, we’ll get to that later.

Now that all the options are initialized, you can create a “`char`” which we’re really just going to use to store binary data.

~~~cpp
char options = 0;
~~~

This is where it all comes together. Bitwise comparisons can set specific bits on and off, using the options variables that we just created earlier. So, if you use Bitwise OR:

~~~cpp
options |= option1;
~~~

What’s really happening is this:

~~~
options: 0000 0000
option1: 0000 0001
------------------
options: 0000 0001
~~~

It compares the two bytes, and if any of the bits are on in either of those bytes, they are turned on in the result. For example, this would be the result of another two random bytes:

~~~
byte1: 1010 1100
byte2: 0001 1110
----------------
outpt: 1011 1110
~~~

This means that Bitwise OR can be used to turn our individual “booleans” on. How would you disable them? Another Bitwise operator, Bitwise AND, and the inversion of the option we’re turning off.

~~~
options &= ~option3;
~~~

How it works:

~~~
 options: 0000 0100
~option3: 1111 1011
-------------------
 options: 0000 0000
~~~

Bitwise AND only produces an output of 1 on a bit when both bits in both of the input bytes are on. By using the inverse of the option (done by the key symbol tilde), this ensures that all other options that were enabled stay enabled, but the selected one to be deactivated will 100% of the time be turned off. Again, here’s another example.

~~~
bool1: 1001 0110
~bool: 1110 1111
----------------
outpt: 1000 0110
~~~

This is similar to how a bit mask works, but I’ll follow that up in another post. Finally, to compare whether a bool is on or not, you can simply use a Bitwise & with the normal option to check if it’s + or 0, and then use a static cast to make it a boolean, like so:

~~~cpp
if (static_cast<bool>(option & option4)) {
	std::cout << "Hey, option 4 is on!\n";
}
~~~

But there’s a much easier way to do this, that doesn’t require fiddling around with raw binary values. This was more just a way to understand it than how it should actually be implemented. Here’s the real, built-in method, provided by C++’s standard library.

## The std::bitset Method
This method requires the use of a library, but is arguably much better. To start, import the bitset library from system.

~~~cpp
#include <bitset>
~~~

Once this is done, you can use std::bitset<int> to create a new set of bits available for boolean use. There are several key commands that carry out the features of doing this manually, which are all here:

{{<notice "" "Remember to `include <iostream>` if you’re planning to output text like in these examples, and follow good practice by leaving out `using std`.">}}

~~~cpp
std::bitset<8> options;
options.set(8); //Turns the 8th bit on.
options.reset(8); //Turns the 8th bit off.
options.flip(8); //Flips the 8th bit.
options.test(8); //Tests if bit 8 is on, returns an int.

if (static_cast<bool>(options.test(8))) {
	std::cout << "Static casting allows for use in IF blocks.\n";
}
~~~

That’s much easier, right? So, now you know the mechanics of how it works, and the bit-level inputs required, go check it out.

Thanks for reading!
