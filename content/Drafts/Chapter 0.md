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

# Programming Methodology --- Beyond C

Taking a step back from C, computers, and all the nitty gritty details for second, there's a separate concept we need to talk about: Programming.

It might go without saying that programming is a tool, a means to an end. And there are concepts that are related to programming that are not exclusive to C. 

Here's an analogy: Let's say we wanted to take photos of something. That's simple right? We could just use a camera, that's our **tool**. Except now there's the question of what kind of camera do you want to use? A Nikon? A Canon? 


![[d3500.jpg|350]] ![[canon-t7.png|250]]

Both of these cameras would get the job done, but **learning how to use the camera** isn't all there is to **learning how to take pictures**. Learning how to use the camera might be stuff like learning where all the buttons are, how to change the zoom on the lens, navigating the menu. These differ from camera to camera. But there are also deeper concepts that aren't exclusive to the camera you're using that you need to learn: Shot composition, knowing how lighting, exposure, shutter speed affect the outcome of the picture, and so on. These things exist as concepts beyond the camera that you'll need to know.

**That said**, the best way to learn is to still pick up a camera and use it to take pictures. So along the way, you'll learn about how to use the camera, but also through it, an instrument for other general concepts.

Similarly, in programming, especially for beginners, you'll need to pick up a few things at once: a programming language (that's the camera), but also programming methodology (that's the concepts that aren't necessarily tied to a specific language).

## Learning to Program in General

Having said that, we recommend bearing a few things in mind when picking up your first programming language, think of these as helpful things to focus on (consciously) to speed up your learning process.

![[mindful.gif]]


#### Understanding the difference between learning C features, and general programming methodology
As we've mentioned, there is a difference between learning C itself, versus learning programming itself. And it's very easy and common to conflate the two things. If you're in it for the long haul, and the long run, you need to understand that good programmers are never tied to any single language. You might have a favourite or a language that we are most proficient in, but eventually you'll need to graduate beyond just being a one-trick pony and being able to code in a few languages.

Why? Different programming languages offer different advantages (and also disadvantages). If you want to pick the right tool for the job, you need to be able to use the tool in the first place.

Quick and dirty one-off scripts for parsing and processing text? You'd probably be better of using Python instead of C. Want to write concurrent programs? You should probably consider using Go. Want to write a logic behind a web page? Then perhaps JavaScript.

**Being clear on programming methodology lets you transfer your skills across languages faster**.

#### Getting Your Hands Dirty, and Carefully Planning It Out
Programming really isn't an "on-paper" thing. Throughout the course we'll be talking a lot about thinking things through and making game plans before writing code. Lots of people tend to spend too much time on the "thinking" part and not actually write any code.

Both parts are important! It's important to plan things through, it's also very important to actually get your hands dirty and write the code. **Feel** the code through your fingertips.
#### Learning to Read Error Messages (and Getting Comfortable With Them)
Making mistakes are going to be common, and there will be times where your compiler will try to be helpful by giving error messages. (This is not limited to C) And it will be tempting to ignore them considering how it will often involve words and jargon you're not familiar with.

But learning to read them and letting them help hint at you at what's going on will help you speed the process up.
#### Learning to Debug
Again, making mistakes is going to be common. And like it or not, you'll almost definitely be debugging your programs. Understand that it's part of the process! And while it might be painful (especially when it's because your programs aren't working), it's something even good programmers have to do.

Eventually as you get more and more experience, systems that you use get more and more complicated. Debugging is a useful skill that you should hone. Trust the process.

#### Reading Manuals
We can't teach you all there is to know about everything in programming. Also, we can't show you the entire C standard library, let alone other well-known (or even lesser-known) libraries out there. Getting used to reading manuals and documentation is how you'll learn to be independent.

#### IDEs and Tooling


#### Using LLMs (Why and When Not To)
