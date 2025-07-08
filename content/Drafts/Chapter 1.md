---
title: "Chapter 1: Introduction, How Computers Work, Memory Layouts, Data Types and Operations"
---

This chapter is going to be a doozy. We'll start off by priming you with some of the prerequisite knowledge you need to know surrounding C.

Let's start off with a snippet that we'll be using throughout this chapter.

```C
#include <stdio.h>
int main(int argc, char **argv){
    printf("hello world\n");
    return 0;
}
```

This is most probably everyone's first C program. There's a lot to cover, and for today it's a whirlwind tour around all the important aspects you need to know surrounding this program. As an overview, we'll be covering:

1. How to create an executable out of written C code.
2. C Code Compilation.
3. A simple mental model of a process, and computer memory.
4. Data types in C, and their operations.

Again, it's quite a few disparate topics, so we'll be dipping our toes only a little bit in every topic.

# Creating programs from C code

So let's say we had that snippet written down somewhere. How do we actually "run" the code? There are many ways we can get this down, but here's one of the simplest ways: An online compiler called [Godbolt](https://godbolt.org).  We've used their sharing feature to actually already pre-write in the snippet for you, so you can pop open the site [here](https://godbolt.org/z/d7oK4sKEM). If you visit it, you should be greeted by this on the page.

![[godbolt-hello-world.png]]

On the left pane is where you'd write code, and the website will actually automatically try compiling whatever has been written in it. For now, since it has been pre-filled with our snippet, it has automatically compiled the the code. On the bottom right pane, you'll see the following:

```
Program returned: 0
Program stdout
hello world
```

Ignoring the first 2 lines for now, you'll notice that the program has somehow output "hello world".

Let's look at the most likely line that made this happen: **line 4**. It reads `printf("hello world\n");`. What's that all about?

`printf` stands for "print format", and this is a **function** that we will **call** to output stuff to the screen.

![[function-syntax.svg]]

We'll talk more about functions in a little bit. For now, just understand that:

1. `printf` is the name of a function.
2. To **call** the `printf` function, we write the name, followed by `()`. Like `printf()`.
3. To pass inputs into `printf`, we do so by putting it within the `()`.

>[!Try-It!]+
> 1. Open up Godbolt with our snippet [here](https://godbolt.org/z/d7oK4sKEM).
> 2. Change `"hello world"` to whatever you like.
> 3. Wait a few seconds for the website to compile the new code.
> 4. See how the output has changed.
>    
> **Few things to try and take note:**
> What happens if we forget the `;`? I.e. what happens if we changed the line to:
> ```C
>printf("hello world\n")
>```
> What does Godbolt tell us?
> 
> ---
> Can you have the input in multiple lines? I.e. what happens if we tried something like:
> ```C
> printf("hello
> world");   
> ```
> What does Godbolt tell us?
> 
> ---
> What happens if we tried to get the program to output just backslash (i.e. `\`). What happens if we wrote something like:
> ```C
> printf("\");
>```
> What does Godbolt tell us?

So we've made a few C programs. But what did it mean to make them? What did Godbolt do?

## Compilation

If you remember what we mentioned in [[Chapter 0]], Godbolt here has taken what we've written, and used a compiler on it (in this case, the compiler's name is GCC). The compiler looks at our code, and outputs **assembly code** out of it. This is what the CPU will see and run.

> Does this mean that the CPU does not run our C code directly?

Yep, that's right! Think of the compiler as the program that understands the CPU better than we do, and hence it's the one who reads our C program and figures out what to tell the CPU to run on our behalf.

![[compilation-process.svg]]

So on the top right pane of the page, in case you're curious, you can see the assembly that is a result of your C program. Don't worry, you don't have to understand it, but just know for now that this is part of how your program is created, and what the CPU sees.

By the way, the compilation process is quite involved and at some point we will be talking about different aspects of it when you understand more, but for now, this simple mental picture suffices.

Eventually, we will also show you how to invoke the compiler yourself.

# How Computers Work

While we're not a course on computer organisation or architecture, since you're learning C, there is some amount of background knowledge you're going to need to know about computers. While covering a realistic depiction of modern CPU architectures is in and of itself worthy of a full course, a simpler model for computers will suffice for us.

![[computer-organisation.svg]]

You might want to think of a computer as having 2 parts for now: A CPU, and a Memory region (this ignores a lot but it makes the picture a lot simpler). Don't worry about what the sub-parts are, we will get around to those in due time. Think of a CPU as really just reading instructions from memory, executing instructions, and at times reading and writing other kinds of data to memory as well.

<!-- should we give an example with assembly? --> 

