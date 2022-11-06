---
Lecture: 1
Title: C
Date: 2022-11-04
---
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
