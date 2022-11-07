# C
### -C is a programming language that has all the features of Scratch and a little less friendly since it's purely in text

###### Our first program in C that simply prints "hello, world" to the screen looks like this:

```C
#include <stdio.h>

int main(void)
{
	printf("hello, world\n");
}
```

# IDEs, compilers, interfaces

#### -In order to turn this code into a program that our computer can actually run, we need to first translate it to binary.
#### -Tools called IDEs, [**integrated development environments**](https://en.wikipedia.org/wiki/Integrated_development_environment), will include features for us to write, translate, and run our code.
#### -One popular IDE, [Visual Studio Code](https://code.visualstudio.com/), contains a text editor or area where we can write our code in plain text and save it to a file:

![VS Code C](https://cs50.harvard.edu/x/2022/notes/1/text_editor.png)

#### - Now our **source code**, or code that we can read and write, is saved to a file called `hello.c`. Next, we need to convert it to **machine code**, or zeroes and ones that represent instructions that tell our computer to perform low-level operations.
#### - A compiler is a program that can convert one language to another, such as source code to machine code:

![Compiler Image](https://cs50.harvard.edu/x/2022/notes/1/compiler.png)

#### - Visual Studio Code, also referred to a VS Code, is typically a program that we can download to our own Mac or PC. But since we all have different systems, it’s easier to get started with a cloud-based version of VS Code that we can access with just a browser.
#### - In the bottom half of the VS Code interface, we see a ***terminal***, a window into which we can type and run text commands.
#### -This terminal will be connected to our own virtual server, with its own operating system, set of files, and other installed programs that we access through the browser.
#### - The terminal provides a **command-line interface**, or CLI, and it allows us to access the virtual server’s operating system, [Linux](https://en.wikipedia.org/wiki/Linux).
#### -We’ll run a command to compile our program, `make hello`. Nothing appears to happen, but we’ll now have another file that’s just called `hello`, which we can run with `./hello`:

![Hello](https://cs50.harvard.edu/x/2022/notes/1/hello_world.png)


#### - `./hello` tells our computer to find a file in our current folder, called `hello`, and run it. And we indeed see the output that we expected.
#### -  We’ll open the sidebar and see that there are two files in our virtual server, one called `hello.c` (which we have open in our editor), and one called `hello`:

![Folder or Repository CS50](https://cs50.harvard.edu/x/2022/notes/1/sidebar.png)

###### - The `make hello` command created the `hello` file containing machine code.
###### -The sidebar is a graphical user interface, or GUI, with which we can interact visually as we typically do.

#### - To delete a file, for example, we can right-click it in the sidebar and select the “Delete Permanently” option, but we can also use the terminal with the `rm` command:

![rm](https://cs50.harvard.edu/x/2022/notes/1/rm.png)

###### - We run `rm hello` to remove the file called `hello`, and respond `y` for “yes” to confirm when prompted.
#### - We can also run the `ls` command to _list_ files in our current folder. We’ll compile our file again and run `ls` to see that a file called `hello` was created: 

![ls](https://cs50.harvard.edu/x/2022/notes/1/make_hello.png)

###### - `hello` is in green with an asterisk, `*`, to indicate that it’s executable, or that we can run it.
#### - Now, if we change our source code to read a different message, and run our program with `./hello`, we won’t see the changes we made. We need to compile our code again, in order to create a new version of `hello` with machine code that we can run and see our changes in.
###### - `make` is actually a program that finds and uses a compiler to create programs from our source code, and automatically names our program based on the name of the source code’s file.

# Functions, Arguments and Return Values

```C
printf("hello, world");
```

#### - The `f` in `printf` refers to a “formatted” string, which we’ll see again soon. And a **string** is a number of characters or words that we want to treat as text. In C, we need to surround strings with double quotes, `""`.
#### - The parentheses, `()`, allow us to give an argument, or input, to our `printf` function.
#### - Finally, we need a semicolon, `;`, to indicate the end of our statement or line of code.

#### - One type of output for a function is a **side effect**, or change that we can observe (like printing to the screen or playing a sound):

![side effect](https://cs50.harvard.edu/x/2022/notes/1/side_effects.png)


#### - In contrast to side effects, we also saw functions, with **return values** that we can use in our program. That return value might then be saved into a **variable**.

```C
string answer = get_string("What's your name? ");
```

#### - In C, we have a function called `get_string()`, into which we pass the argument `"What's your name? "` as the prompt.

#### - Then we save the return value into a variable with `answer =` . Here, we’re not asking whether the two sides are equal, but rather using `=` as the **assignment operator** to set the _left_ side to the value on the _right_.

>  If we to set a value with a different type to a variable, the compiler will give us an error.

#### - We'll experiment again with our original program, this time removing the `\n` from string we pass into `printf`:

```C
#include <stdio.h>

int main(void)
{
	printf("hello,world");
}
```

#### - And now, when we compile and run our program, we won’t have the new line at the end of our message:

```
$ make hello
$ ./hello
hello, world$
```

#### - Let's try adding a new line within our string:
```C
#include <stdio.h>

int main(void)
{
	printf("hello, world
	");
}
```
#### - Our compiler will gives us back many errors:

```
$ make hello
hello.c:5:12: error: missing terminating '"' character [-Werror,-Winvalid-pp-token]
    printf("hello, world
          ^
hello.c:5:12: error: expected expression
hello.c:6:5: error: missing terminating '"' character [-Werror,-Winvalid-pp-token]
    ");
    ^
hello.c:7:2: error: expected '}'
}
^
hello.c:4:1: note: to match this '{'
{
^
4 errors generated.
make: *** [<builtin>: hello] Error 1
```

> Since many of these tools like compilers were originally written years ago, their error messages are concise and not as user-friendly as we’d like, but in this case it looks like we need to close our string with a `"` on the same line.

#### - `\n` is for creating a new line,is for using an ***escape sequence***, or a way to indicate a different expression within our string. In [[C]], escape sequences start with a backlash, `\` .

#### - Writing a program to get a string from the user:

```C
#include <stdio.h>

int main(void)
{
	string answer = get_string("What's your name? ");
	printf("hello, answer\n");
}
```

##### - We add a space instead of a new line (`\n`) after `What's your name? ` so we can type our name in the same line.

##### - When we compile `make hello`, we get a lot of errors:
```
$ make hello
hello.c:5:5: error: use of undeclared identifier 'string'; did you mean 'stdin'?
    string answer = get_string("What's your name? ");
    ^~~~~~
    stdin
/usr/include/stdio.h:137:14: note: 'stdin' declared here
extern FILE *stdin;             /* Standard input stream.  */
            ^
```

###### -`hello.c:5:5` indicates that the error was found on line 5, character 5. It looks like a string isn't defined.

#### - ***There're amount of functions or features that don't come with ***C*** so we need to load libraries.

## Library
### : is a common set of code that we can reuse and `<stdio.h>` refers to a library for standard input and output functions. With the line `#include <stdio.h>`, we're loading this library that contains `printf`. 

#### - We need to use another library called `<cs50.h>`, a library written by the CS50'staff, with helpful functions and definitions like `string` and `get_string`.

> Like this:

```C
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string answer = get_string("What's your name? ");
    printf("hello, answer\n");
}

```

#### - When we run our program, we see `hello, answer` printed literally:

``` 
$ make hello
$ ./hello
What's your name? David
hello, answer
$
```
#### - We need to use more syntax:

```C
printf("hello, %s\n", answer);
```
###### - With `%s`, we are adding a placeholder for `printf` to format our string.

### - IDEs for programming languages will helpfully highlight, different ideas in our code:

![Highlighted syntax](https://cs50.harvard.edu/x/2022/notes/1/highlighting.png)

###### - With this is easier for us to see the different components of our code and notice when we make a mistake.

#### - We could also use the return value from `get_string` as an argument.

```C
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    printf("hello, %s\n", get_string("What's your name? "));
}
```

#### - But for most of people this might be harder to read and we aren't able to reuse the return value later.

#### - `get_string` in **C** is a function that has a return value as output:

![arguments-functions-return value](https://cs50.harvard.edu/x/2022/notes/1/return_value.png)

# Main, Header Files and Commands

#### - In **C**, `main` achieves a similar effect as the Scratch block "when the green flag is clicked".

```
int main(void)
{

}
```

###### - The curly braces, `{` `}`, surround the code that will run when our program is run as well.

#### - ***Header Files***, like `stdio.h` tells our compiler which libraries to load in our compiler; a library store a lot of functions and features like `printf` that we can use in our code.

#### - In [Linux](https://en.wikipedia.org/wiki/Linux "Linux"), there are commands we might use:

* `cd`, for changing or current directory (**folder**)
* `cp`, for copying files and directories
* `ls`, for listing files in directory
* `mkdir`, for making a directory
* `mv`. for removing or renaming files and directories
* `rm`, for removing(deleting) files
* `rmdir`, for removing(deleting) directories

#### We can use the GUI and the Terminal to be able to create new files and folders:

###### With the terminal: 

```
$ mkdir pset1
$ mkdir pset2
$ ls
hello*  hello.c  pset1/  pset2/
$
```

###### -We'll run `mkdir` to create a new folder. Then we can run `ls` to see our current directory has the new folder.

###### - Now, we can run `cd` to change our directory: (`cd`: change directory) : 

```
$ cd pset1/
pset1/ $ ls
pset1/ $
```

###### - We can make another directory with `mkdir` and change into it with the command `cd`:

```
pset1/ $ mkdir mario
pset1/ $ ls
mario/
pset1/ $ cd mario/
pset1/mario/ $
```

###### - We run a specific command to VS Code, `code mario.c`, to create a new file. We see it in the sidebar with our folders and files:

![Code Mario.c](https://cs50.harvard.edu/x/2022/notes/1/sidebar_mario.png)

###### - To change our current directory to the parent directory, we can run `cd ..` We can up to levels at once with `cd ../..` as well:

```
pset1/mario/ $ cd ..
pset1/ $ cd mario/
pset1/mario/ $ cd ../..
$
```

###### - We we run the command `cd` will also bring us back to our default directory:

```
pset1/mario/ $  cd
$
```

# Types, Format Codes and Operators

### - There are many Data Types we can use for our variables, which indicate to our program what type of data they represent:

#### - `bool`, a Boolean expression of either `true` or `false`
#### - `char`, a single character like `a` or `2`
#### - `double`, a floating-point value with more digits than a `float`
#### - `float`, a floating-point value, or real number with a decimal value
#### - `int`, integers up to a certain size, or number of bits
#### - `long`, integers with more bits, so they can count higher than an `int`
#### - `string`, a string of characters
#### - ....

### - The CS50 library has corresponding functions to get input of various types:

#### - `get_char` 
#### - `get_double`
#### - `get_float`
#### - `get_int`
#### - `get_long`
#### - `get_string`
#### - ....

### - For `printf`, too, there are different placeholders for each type called ***format codes***.

#### - `%c` for chars
#### - `%f` for floats or doubles
#### - `%i` for integers
#### - `%li` for long integers
#### - `%s` for strings

#### - There are several mathematical ***operators*** we can use, too:

#### - `+` for addition
#### - `-` for substraction
#### - `*` for multiplication
#### - `/` for division
#### - `%` for remainder

# Variables, syntactic sugar
#### - We might create a variable called `counter` and set its value to `0` in [[CS50 WEEK 1#C|C]] with the following:

```
int counter = 0;
```

#### - And we can increase the value with: 

```
counter = counter + 1;
```
###### - In [[CS50 WEEK 1#C|C]] we’re taking the original value of `counter`, adding 1, and then assigning it into the left side, or updating the value of `counter`.
###### - We don’t need to specify the type of `counter` again, since it’s been created already.
###### -C also supports **syntactic sugar**, or shorthand expressions for the same functionality. We could equivalently say `counter += 1;` to add one to `counter` before storing it again. We could also just write `counter++;`, or even `counter--;` to subtract one.

###### - Adding:
```
counter += 1;
```

```
counter ++;
```

###### - Substracting: 
```
counter --;
```
# Calculations:

#### - Let's create a new file with the command `code calculator.c` in the terminal. Then, we’ll add in the following code to the editor that’s opened for us, and save the file:

```C
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int x = get_int("x: ");
    int y = get_int("y: ");
    printf("%i\n", x + y);
}
```

#### -   We’ll prompt the user for two variables, `x` and `y`, and print out the sum, `x + y`, with a placeholder for integers, `%i`.
#### - These shorter variable names are fine in this case, since we’re just using them as numbers without any other meaning.

#### - We can compile and run the program with:

```
$ make calculator
$ ./calculator
x: 1
y: 1
2
```

#### - We change our program to use a third variable, `z`:

```
int z = x + y;
printf("%i\n", z);
```

###### - This version gives us a reusable variable, but we might not intend on using the sum again in our program, so it might not necessarily be better.

#### - We put comments (notes to ourselves that the compiler ignores) inside of our code. Comments start with, `//`:

```
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    // Prompt user for x
    int x = get_int("x: ");

    // Prompt user for y
    int y = get_int("y: ");

    // Perform addition
    printf("%i\n", x + y);
}
```

###### - The Comments can be very useful for us when our code is to complicated, we’ll find these comments useful for reminding ourselves what and how our code is doing.

#### - In the terminal window, we can also start typing commands like `make ca`, and then press the `tab` key for the terminal to automatically complete our command. The up and down arrows also allow us to see previous commmands and run them without typing them again.

###### - We’ll compile our program to make sure we haven’t accidentally changed anything, since our comments should be ignored, and test it out:

```
$ make calculator
$ ./calculator
x: 1000000000
y: 1000000000
2000000000
$ ./calculator
x: 2000000000
y: 2000000000
-294967296
```

#### - As you can see, Data Types each use a fixed number of bits to store their values. An `int` in our virtual environment uses 32 bits, which can only contain about four billion (2<sup>32</sup>) different values. But since integers can be positive or negative, the highest positive value for an `int` can only be about two billion, with a lowest negative value of about negative two billion.

#### - We can change our program to use `long` to use more bits:

``` C
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    // Prompt user for x
    long x = get_long("x: ");

    // Prompt user for y
    long y = get_long("y: ");

    // Perform addition
    printf("%li\n", x + y);
}
```

###### - But we could still have a value that’s too large, which is a general problem we’ll discuss again later.
