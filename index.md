# c-stem

## What is a program?

text

## Compiling

text

## It's all about blocks

text

Among few other things, a `C` program is mostly made of blocks of code called "functions". Very similarly to how we defined a program before, these blocks are a way to group together lines of code that are related to each other. Like a program, they can have inputs, an output, and may perform side effects. It's not far from reality to understand a function as a small program in itself.

We will come back to functions later in great details, including why they are called "functions", and how to create and use them. For now, let's forget about them except for a very specific one: the `main` function. This particular block of code is extremely important when writing a `C` program: it is what is called the "entry point" of the program.

This is an "as short as reasonable" example of a `main` function:

```c
int  main() {
  return 0;
}
```

It can be compiled and run, even though it doesn't do anything useful:

```shell
$> ls
main.c
$> cat main.c
int  main() {
  return 0;
}
$> cc -o main main.c
$> ls
main
main.c
$> ./main
$>
```

Let's study the program's syntactic constituents:
- Line 1: `int` is called a "type". Here, it defines the "type" of the output of this function. We will dive into `C` types later in great details, but for now, all you have to understand about this `int` is that it defines what kind of information this block of code will output as a result after execution. The type `int` stands for "integer", which are the ordinary "whole" numbers you are familiar with, like 0, 1, 2, 3, etc. Therefore after execution, this block of code outputs an integer number.
- Line 1: `main` is the name of the function.
- Line 1: `()` is actually an empty pair of braces `(` and `)`. When a function has inputs, these inputs and their type are listed between the braces. This specific example of a `main` function does not have any input.
- Line 1: `{` (prenounced "left curly brace") marks the start of a block of code that is closed by the corresponding right curly brace `}`.
- Line 2: `return 0;` is our first proper line of `C` code! It has 3 elements:
  - `return` is an instruction used to finish the execution of a function. It is effectively "returning" from the current function being executed to the one that "called" it. Calling functions and returning from functions are interesting topics that we will address later. For now, since the `main` function is where the program starts, when "returning" from this function actually makes the program end.
  - `0` is just the number 0, however placed next to `return`, it means that the function will actually send back, or "return" that value to whatever start its execution. Since using `return` in the `main` function ends the program, the value `0` becomes the actual output of the program.
  - `;` is a semicolon. Semicolons are use to indicate the end of a line of `C` code. As a beginner, it can be confusing as to when to add a ";" at the end of a line or not. Let's not think to much about for now.
- Line 3: `}` is the matching curly brace from line 1, effectively closing the definition of the `main` function.
