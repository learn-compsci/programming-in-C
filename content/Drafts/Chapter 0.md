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

>[!Intructions 1]
>1. Walk to "Aft Bt Timah Rd" bus stop.
>2. Take the 151 bus.
>3. Get off at Ctrl Lib.

Which seems reasonable, assuming your friend speaks English, I think they got the idea. Now let's pretend that your friend is actually new to Singapore, so they don't yet know how to take public transport. They have an EZ-Link card, but otherwise just don't have the know-how.

How would the instructions change? Well our previous steps probably would not suffice anymore, your friend probably still would not quite know what to do (aside from say... walking to the bus stop).

So instead, we might have to "translate" our initial set of instructions, into something like the following instead:

> [!Intructions 2]
> 1. Walk to "Aft Bt Timah Rd" bus stop.
>2. When you see the 151 bus approaching, stand at the side of the road, and raise your left hand to flag down the bus.
>3. Enter via the front door, and press your EZ-Link card against the reader, it should beep and flash green.
>4. Find a place to either sit or stand while on the bus.
>5. Press the red button when the next stop is Ctrl Lib.
>6. When the bus has stopped, tap your EZ-Link card again at the reader in the middle of the bus.
>7. Exit the bus via the door in the middle of the bus.

Wow! That's much longer isn't it? You might notice that the new steps 2 through 4 basically correspond to "Take the 151 bus", while the remaining steps after that correspond to "Get off at Ctrl Lib".

So what's going on here? We can think of the first set of instructions as the "high-level" idea of what needs to be done. On the other hand, the second set of instructions are more "low-level", it's a lot more detailed, and a lot more verbose.

> But what does this have to do with C programming?

The idea is that we want to express our ideas in a (borderline) readable language. Notice that we then aren't ourselves directly telling the CPU what to do, but rather expressing our intent. So again, we might write something like:

```C
#include <stdio.h>

int main(int argc, char **argv){
	printf("hello world\n");
	return 0;
}
```

Then, something called a **compiler** actually takes this code, and outputs the following:

```x86
.LC0:
.string "hello world"
main:
push rbp
mov rbp, rsp
sub rsp, 16
mov DWORD PTR [rbp-4], edi
mov QWORD PTR [rbp-16], rsi
mov edi, OFFSET FLAT:.LC0
call puts
mov eax, 0
leave
ret
```

So the compiler takes our "high level" ideas, and translates it into "low level" instructions that the CPU can actually understand.

> This all sounds awfully complicated, so why do we do this?

I'm glad you asked! There are a few reasons why this is a thing. We won't list all of them, but here are the main important ones you should know:

1. **Portability**: One thing we've not mentioned, is how you could write the same C code, and have it work across different CPUs. The instructions we've shown above are for the x86 architecture, but if we had work with different types of CPUs, like an ARM CPU or a RISC-V CPU, then would have to re-write the instructions, since they're different.
   
   On the other hand, you could just have the same C code, and have the compiler deal with the nitty gritty of figuring out what is the correct set of instructions to use, to translate your program into. This way, you can write just one program in C, and run it on any possible machine without having to know what CPU it uses.
   
2. **Optimisations**: Since the instructions are exactly what the CPU follows, you might actually want to trust that if you gave C code to your compiler, your compiler would write better instructions than you might if you were to hand write the instructions yourself. This is one of the few reasons why C/C++ is regarded as a "fast" programming language!

The takeaway is this: Technically a computer program is a set of instructions that tell the computer what to do. **Your C code**, is a way of telling the computer what to do. The **compiler**, takes your instructions, and translates it to instructions the computer can actually understand.

% Insert Drawing of Idea Here

# The C Programming Language and Why C

The C programming language is an **imperative** programming language, where you're free to manage your own memory allocations, have access to raw addresses, and has limited language features (and is thus a little simpler, and easier to learn).

C gets a bad reputation for being the language that (among other things):

1. Has too many "footguns" to shoot yourself in the foot with.
2. The idea of "segfaulting" from not managing your pointers/memory accesses well.
3. Lacking too many language features and is thus not "ergonomic".

And some of these criticisms are fair! Though there really is no such thing as a perfect programming language.

But hear us out, there are still reasons why C is a language you should learn and know.

### Proximity to hardware
C is probably the most widely used language when it comes to bare metal programming. Also, a lot of device drivers (like for your network card, sound card, graphics processing unit) are also usually written in a language like C, where everything is stripped away, and you're as close as it gets to looking at raw bytes and memory addresses.

In fact, speaking of lack of environments, your operating system (which is literally an **environment** for your user programs), be it Windows, MacOS, or Linux, is written in C!

In some sense, sometimes you don't have an environment because you might be the one making it!

### Fine Control and Performance Boosts
The lack of overhead (because you have to manually manage everything yourself) does mean you get a lot of control over how much memory you're using, as well as the kind of and amount of operations you're doing. This, combined with the lack of overhead (from additional fluff that you'll have to run), really lets you write performant programs in C.

Another reason why it's easier to write performant programs in languages like C or C++, is the fact that your typical C compilers like GCC or Clang have a lot of optimisation techniques ready at hand to optimise your code.

### Widespread Use in Low-Level Systems
Think of it this way: If you need to work with existing low level systems and read their code, or if you are joining a team that works on high performance computing, chances you are going to have to be able to read C.

# Programming Methodology