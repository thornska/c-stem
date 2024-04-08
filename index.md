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
- Line 1:
  - `int` is called a "type". Here, it defines the "type" of the output of this function. We will dive into `C` types later in great details, but for now, all you have to understand about this `int` is that it defines what kind of information this block of code will output as a result after execution. The type `int` stands for "integer", which are the ordinary "whole" numbers you are familiar with, like 0, 1, 2, 3, etc. Therefore after execution, this block of code outputs an integer number.
  - `main` is the name of the function.
  - `()` is actually an empty pair of braces `(` and `)`. When a function has inputs, these inputs and their type are listed between the braces. This specific example of a `main` function does not have any input.
  - `{` (prenounced "left curly brace") marks the start of a block of code that is closed by the corresponding right curly brace `}`.
- Line 2:
  - `return 0;` is our first proper line of `C` code! It has 3 elements:
    - `return` is an instruction used to finish the execution of a function. It is effectively "returning" from the current function being executed to the one that "called" it. Calling functions and returning from functions are interesting topics that we will address later. For now, since the `main` function is where the program starts, when "returning" from this function actually makes the program end.
    - `0` is just the number 0, however placed next to `return`, it means that the function will actually send back, or "return" that value to whatever start its execution. Since using `return` in the `main` function ends the program, the value `0` becomes the actual output of the program.
    - `;` is a semicolon. Semicolons are use to indicate the end of a line of `C` code. As a beginner, it can be confusing as to when to add a ";" at the end of a line or not. Let's not think to much about for now.
- Line 3:
  - `}` is the matching curly brace from line 1, effectively closing the definition of the `main` function.

## The secret ingredient is crime

It is possible to send inputs to a program on the command line, like `./my_program arg0 arg1 arg2`. Unfortunately, doing so requires to understand several topics that we haven't addresed yet. This is quite crippling, because we are stuck with writing programs that can't take any input.

But we can cheat.

The compiler has a particular option `-D` that will allow us to replace a pattern of characters of our choice with anything we want in a source file. For instance, if I compile a file `program.c` like so: `cc -o program -D'$VALUE=0' program.c`,  the compiler will search the file `program.c` for every instances of the pattern `$VALUE` then replace them with `0` before actually compiling the file.

Here is an example:
```shell
$> cat cheat.c
int main() {
  return VALUE;
}
$> cc -D'$VALUE'=0 cheat.c && ./a.out ; echo $?
0
$> cc -D'$VALUE'=1 cheat.c && ./a.out ; echo $?
1
```

What we are actually doing here is abusing the "macro" system of the `C` "preprocessor". It's ugly and it has many flaws, but for now it will provide us with a way of simulating numeric inputs to our program.

## Variables

As your programs will grow, you will need to be able to store some values. For example, you might need to save an intermediate result of a complex calculation and refer to this result through a meaningful name later on. That's exactly what variables are for.

In order to store a value, a variable must be of the same "type" as this value. This is the same word "type" that we used earlier when describing the output type `int` of the `main` function. It's still too early to dive into a detailled `C` data types explanation for now, but we can introduce some very important notions to understand about types:

- **Meaning**: a type defines the meaning of a value of that type. So far, we have encountered the type `int` only, and we know that it stands for an interger, a whole number. Therefore, whe know that any value of type `int` in a program must be understood as a whole number in the mathematical sense of the term, and not, say, a phone number or a bank acccount number although they might look like a whole numbers.

- **Operations**: a type also defines the operations that are possible on values of that type. For example, it makes sense to perform an addition on two integer numbers: `2 + 3` equals `5`. However, adding two phone numbers or two bank account numbers does not.

- **Size**: In `C`, types also define the size in bytes that a value of this type will hold in memory. We don't have to understand what a "byte" is for now, and it's enough to understand "one byte" as "one unit of memory". The basic types of `C`, like the `int` type, have an arbitrary size that is defined by the language itself. There are not that many basic types, and remembering their size is easy for the most common ones. In the case of `int`, its size is `4` bytes. This means that any value of type `int` will use 4 "units of memory", regardless if that value is 0 or a very large number. However, the fixed size of a type introduces a limitation: the number of values representable within that size is not infinite. We'll get back to this last comment later when we'll discover how values are actually encoded in the memory.
