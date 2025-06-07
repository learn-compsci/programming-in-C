---
title: "Chapter 0: Computer Programs, The C Language,  Why C, and Programming Methodology"
---

# Amazing Computer Programs and How To Write Them

While tech and programming may seem like all the craze these days, it's definitely not a new thing, programming has been around for a long time, and nowadays it almost seems like you can't get by without knowing how to. This world is vast as it is deep, and there is always a lot to learn, so hopefully what we have written here is a way to get you started in your programming journey.

## Computer Programs

Incidentally, you might be wondering "What does it mean to program? What is a computer program?". As it turns out, if you had asked this question perhaps, 20 years back, the answer was pretty simple, but nowadays, it's a pretty complicated question to answer.

So the best answer we have for you is:

> You're just trying to tell the computer what to do.

Which sounds pretty obvious (and non-helpful). But as you learn more, you'll end up realising that this is actually the best possible description.

Now, if you're into computer engineering (and/or information security) though, we have a slightly more specific description for you, but it's still a little complicated, bear with us.

![[program-model.svg]]

This picture will change the more you know, but for now it'll suffice. Here's an example of what the computer sees as the **program code** it needs to run:

![[example-assembly.png]]

Think of these as instructions. They literally tell the CPU step by step what needs to be done. On the first column, you'll see **instructions**, such as `push`, or `mov`, or `sub`. And so on. These literally _instruct_ the CPU on what to do. The rest of it are **arguments**. These aren't too important for now, but what you need to know is that this is (almost) exactly what your CPU sees, and has to act on. 

**From this perspective**, a computer program is a sequence of instructions that the CPU runs faithfully.
# The C Programming Language

**On the other hand**, here's what we would write in C to get those instructions:

![[example-C.png]]

When comparing this C code to the sequence of instructions before this, there's many aspects to unpack here.

That looks a lot simpler doesn't it? In fact, doesn't it look a lot more readable? Isn't the **intent** clearer? From this, we can probably at least surmise that the program is going to do something called "print", and it should print the message "hello world".

So what does the computer run? The C code? The instructions? What's the real program here? Technically speaking, you could consider both to be the computer program. That might sound confusing, but it's a really important concept, so let's explain it.
## Compilation

Let's start with an analogy. Pretend for a moment that you had to help your friend go from Beauty World to Central Library (and your friend doesn't know how to use Google Maps). You might tell your friend something like:

1. Walk to "Aft Bt Timah Rd" bus stop.
2. Take the 151 bus.
3. Get off at Ctrl Lib.

Which seems reasonable, assuming your friend speaks English, I think they got the idea. Now let's pretend that your friend is actually new to Singapore, so they don't yet know how to take public transport. They have an EZ-Link card, but otherwise just don't have the know-how.

How would the instructions change? Well our previous steps probably would not suffice anymore, your friend probably still would not quite know what to do (aside from say... walking to the bus stop).



