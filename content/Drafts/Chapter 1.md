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



