% CSC 211 Lab 0: Getting Started
% Spring 2017

#Downloading Docker

###Step 1:

####If you are using your own computer:

Install Docker from the website [Docker Download Page](https://www.docker.com/products/docker#/)

Make sure to choose the correct download for you machine.  If you don't have Windows 10 Pro you or macOS 10.10.3 and above, you need to install the [Docker Toolkit](https://www.docker.com/products/docker-toolbox).

[Windows 10 Docker tutorial](https://docs.docker.com/docker-for-windows/)

[Mac 10.10.3+ Docker tutorial](https://docs.docker.com/docker-for-mac/)

[Linux Docker tutorial](https://docs.docker.com/engine/getstarted/)

Run the Docker installer.  If you are using the Docker Toolkit make sure to install everything (git, VM, etc).

###Step 2:

After installation, open Docker and wait for it to initialize.  Once Docker has finished initializing the command line should be a single `$`.  Test your installation by typing `docker search ndaniels` on the command line.  You should see a few path names, one of them should be `ndaniels/csc211-dev`.

###Step 3:

Type `docker pull ndaniels/csc211-dev` on the command line.  This will install the necessary software you need for this course (clang, git, ruby).  Wait for installation to complete. This will take a few minutes but you should see 

###Step 4:

Type `docker run -t -i ndaniels/csc211-dev` on the command line.  Your command line should change to `[student@docker:~]$`.  This is the command line you will need to run [bash commands](http://ss64.com/bash/) and the programs in this course (instead of Docker commands).

Type `exit` to leave the container.  Your command line should return to a single `$`.

###Step 5:

Create a new folder on your desktop called 'CSC211'.  This is the folder where you will keep your program files.  Now go back into the container you created by typing the following command on the command line according to your operating system below (you may want to double check the file path by right clicking on the folder and checking 'properties'.  Make sure your file path is correct, otherwise you will enter a non existent folder and this will be saved to your VM even though it doesn't exist):

**Windows**

`docker run -t -i -v /c/Users/<Your user name>/Desktop/CSC211:/home/student/data ndaniels/csc211-dev`

*Note*: Replace <Your user name> with the name of your user account on your Windows system.

*Note*: Make sure the 'c' is lowercase in your folder path.  Otherwise, everything is CASE SENSITIVE.

**MAC**

`docker run -t -i -v ~/Desktop/CSC211:/home/student/data ndaniels/csc211-dev`

**Linux**

`docker run -t -i -v <Path to folder>:/home/student/data cscuri/dev-cc-python`

*Note*: Replace <Path to folder> with the path to the CSC211 directory you created. If you're using Linux already, you should be able to figure this out.

Now the desktop folder you created is mapped to `/home/student/data` in your docker container and you can read/write files to that folder.

###Step 6:

To make it easier to run the CSC211 development environment in the future, you will create a command-line *alias*.

If you are on MacOS or Linux, you will use the `alias` feature of the `bash` command shell.

First, Type `exit` to leave the container.  Your command line should return to a single `$`.

Next, type `alias d211="docker run -t -i -v ~/Desktop/CSC211:/home/student/data ndaniels/csc211-dev"`

Now, type `d211` on the command line. It should do exactly the same thing as when you typed the lengthy docker command earlier. But, it won't persist if you quit the Docker application. So, let's fix this. 

Once again, type `exit` and you should be back at the `$` prompt.

Type `echo "alias d211=\"docker run -t -i -v ~/Desktop/CSC211:/home/student/data ndaniels/csc211-dev\"" >> ~/.bash_profile`. This writes the `alias` command into the file `.bash_profile` which ensures that it will make the `d211` alias available whenever you open up a Terminal.

*Note*: If you are on Linux, you'll have to adjust the paths. If you are using a shell other than `bash`, you'll also have to make adjustments that we assume you know how to make.

*Note*: If you are on Windows, for now, you'll need to type the full command `docker run -t -i -v /c/Users/<Your user name>/Desktop/CSC211:/home/student/data ndaniels/csc211-dev` to launch Docker. We are working on a way of simplifying this; bear with us!

#Installing a text editor

In this class, you will use a text editor on your host system (e.g. on MacOS if you use a Mac, and on Windows if that's your preference). Because of that shared CSC211 folder you set up, both your native platform *and* the Linux environment running inside Docker will be able to talk to each other.

If you don't already have a text editor that you know and love, we recommend Github's [Atom](https://atom.io) editor. If you are using a lab machine, it's already installed. If you are using your own machine, you can [install Atom](https://atom.io).

If you decide you dislike Atom, or just want to try something different, you might also try [Sublime](https://www.sublimetext.com) (Mac, Windows, Linux), [Textmate](http://macromates.com) (Mac), [Notepad](https://notepad-plus-plus.org) (Windows), or [BBEdit](http://www.barebones.com/products/bbedit/index.html) (Mac, and the author lives in North Kingstown!).

Download and install Atom or another editor.

##Running a C++ program in Docker

###Step 1:

Open Docker.  Follow Step 5 from 'Downloading Docker' above so that you have the correct folder on your local machine mapped to your Docker container.  As before your command line should look like: `[student@docker:~]$`.  To see what directories and files you can navigate to from your current directory type the command `ls`.  All the files in the current directory should be listed, in this case 'data' should be the only file listed.  Since 'data' is the folder mapped to our local machine, we need to change directories to 'data'.  To change directories type `cd data` and you will be in the data folder.  Now type the command `mkdir lab0` to create a folder (directory) called 'lab0' in the current directory ('data' in this case).  If you created your container correctly you should be able to open the folder on your local machine and see a new folder called 'lab0'.  You should see 'lab0' and any other files you might have created.  Now change directory into 'lab0' by typing the command `cd lab0`.  To print the working directory type `pwd` on the command line and the directory `home/student/data/lab0` should display.

*LPT*: You will be doing a lot of typing. Here's a shortcut. When writing filenames as the argument for a bash command (e.g. the filename 'data' in `cd data`), after typing the initial characters in the filename hit the **tab** button to autocomplete the filename. If it's ambiguous, it'll complete as much as it can; you can type another character to narrow down the search.

###Step 2:

Inside your 'lab0' directory create a new file called 'lab0.cpp' using the command `>lab0.cpp`.  The `>` command pipes any output into the file 'lab0.cpp'.  Since there is no output all this accomplishes is to create a blank file.  The command `echo 'hello world' >lab0.cpp` will print the words 'hello world' into the document.  Now you can open the file anyway you want, from your local machine or using the bash shell.  To view the file using vim type `vim lab0.cpp` and the file will open in the terminal.  To quit vim without saving hit the `esc` key, type `:q!`, then hit the `enter` key.  Here is an [interactive vim tutorial](http://www.openvim.com/).

If you already know vim, or want to learn it, you can use it instead of the text editor you installed previously.

###Step 3:

On your local machine open the folder 'CSC211/lab0' and open the file 'lab0.cpp' with Atom (or another text editor).  Copy and paste the following program into the 'lab0.cpp' file, then save the file:

```
#include <iostream>

int main()
{
  std::cout << "Hello World!\n";
}
```
You now need to compile your program. This turns the human-readable text file you wrote into a set of instructions the machine can execute. We will talk about compilation in the first lecture.
To compile and execute your new program go back to your Docker terminal and type the command `clang -o lab0 lab0.cpp`.  This will create a file called 'lab0' in your 'lab0' folder.  The command `clang` is needed anytime you want to compile a c++ program. The `-o` flag allows you to name the file what you want, in this case 'lab0', and the final argument 'lab0.cpp' is the program you are compiling.  If you don't care to name the file you can use the command `clang lab0.cpp` and a file called 'a.out' will be created automatically instead of 'lab0'.

Now that your program is compiled, check your current working directory to see that the executable file exists.  To execute the file type `./lab0` (or `./a.out` if you did not name your file).  The terminal should print "Hello World!".

##Basic anatomy of a C++ program

###Example 1:

First take a look at the previous example and note that the main function does not have any parameters, and no arguments were passed to the executable file on the command line when running the file.

Next, on your local machine open 'lab0.cpp' with your text editor.  Copy and paste the following program into the 'lab0.cpp' file, then save the file:

```
#include <iostream>

int main(int argc, char* argv[])
{
    std::cout << "Number of arguments: " << argc << std::endl;
    std::cout << "First argument: " << argv[0] << std::endl;
    return 0;
}
```

The program has a few parts.  The first part `#include` is like `import` for Java. It tells the compiler that we want our program to have access to some functions that are provided by the `iostream` library. We need to `#include` the library `<iostream>` to use the `cout` function which prints the output.  The `main` function returns an `int` and has two parameters: `int argc` and `char* argv[]`.  Inside the `{}` is the body of the program and the `return` value is `0` to indicate that the program ran sucessfully.

Compile and run your program as before.  This program will print two things:  The number of command line arguments `argc` and the name of the executable file you used to run the program `argv[0]`.  Since no arguments were passed From the command line, the default option is only one argument: the name of the file used to execute the program. 

###Example 2:

On your local machine open 'lab0.cpp' with a text editor.  Copy and paste the following program into the 'lab0.cpp' file, then save the file:

```
#include <iostream>

int main(int argc, char* argv[])
{
    std::cout << "Number of arguments: " << argc << std::endl;
    std::cout << "First argument: " << argv[0] << std::endl;
    std::cout << "Second argument: " << argv[1] << std::endl;
    std::cout << "Third argument: " << argv[2] << std::endl;
    std::cout << argv[1] << " " << argv[2] << std::endl;
    return 0;
}
```

Compile the code as before, but run the file using the command `./lab0 hello world`.  This time, instead of passing no arguments to the command line, two are passed: 'hello' and 'world'.  Remember, by default there is always one argument in the first position of the array `argv[]` so only two additional arguments are passed to the command line.

*NOTE*: The number of arguments passed on the command line is not the number of parameters in the main function.  We now have three arguments even though only two were passed on the command line, because the name used to run the program is always the first (or "zeroth") argument.

###Example 3

From the last example we can infer that the number of arguments `argc` is the length of the array `argv[]`.  `argc` is an integer and `argv[]` is an array of strings (the type `char*` is pointer to a string of characters, meaning that `argv[0]` dereferences a memory address that points to a string in the first position of the array `argv[]`, `argv[1]` points to the second position, and so on).  So instead of printing out each line separately we can use a `for` loop to print each argument.

On your local machine open 'lab0.cpp' with your text editor.  Copy and paste the following program into the 'lab0.cpp' file, then save the file:

```
#include <iostream>

int main(int argc, char* argv[])
{
    std::cout << "Number of arguments: " << argc << std::endl;
    for (int i = 0; i < argc; i++) {
      std::cout << "Argument " << i << ": " << argv[i] << std::endl;
    }
    
    for (int i = 1; i < argc; i++) {
      std::cout << argv[i] << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

Compile and execute the program with as many arguments as you want.

###Example 4:

Remember that the type `char*` means that each position in the array `argv[]` is a character pointer to the first character in a string.  This means that on top of iterating through each string in the array `argv[]`, we can iterate through each character in each string by starting at the pointer to the first character of each string.  To do this a double array is used `argv[][]` to illustrate how each character in an array of strings can be accessed.

On your local machine open 'lab0.cpp' with a text editor.  Copy and paste the following program into the 'lab0.cpp' file, then save the file, compile it, and run it with some command line arguments:

```
#include <iostream>

int main(int argc, char* argv[])
{
    for (int i = 1; i < argc; i++) {
      int j = 0;
      while (argv[i][j] != '\0') {
        std::cout << argv[i][j++];
      }
      std::cout << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

Notice that to check for termination of each string the character is compared to `\0`.  `\0` is the null terminator symbol and is present at the end of every string in c++.  For this reason the lenght of a string is always one more than the number of characters, e.g 'hello' is a string of length six, not five.  **BEWARE!**

However, it is not necessary to check each character against the null terminator symnol `\0`.  It is sufficient to replace 
`while (argv[i][j] != '\0')` with `while (argv[i][j])` since the condition `argv[i][j]` is false when it is `\0`.

###Example 5:

Another way to access the characters of each string is to use pointer arithmetic.

On your local machine open 'lab0.cpp' with a text editor.  Copy and paste the following program into the 'lab0.cpp' file, then save the file, compile it, and run it with some command line arguments:

```
#include <iostream>

int main(int argc, char* argv[])
{
    for (int i = 1; i < argc; i++) {
      char* charPointer = argv[i];
      while (*charPointer) {
        std::cout << *charPointer++;
      }
      std::cout << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

In this example there is some syntax not introduced yet, particularly `*charPointer`.  We have established that `argv[]` is an array of character pointers, meaning that each position in the array points to the first character of each string in that array.  Before, to access each string in the array, we used the syntax `argv[i]`.  Then, to access any character in a given string we used `argv[i][j]`.  In both cases we are 'dereferecing' the pointer at the index given. `argv[i]` tells the program to dereference the `char*` at position `[i]` of the array `argv[]` and produce the entire string.  `argv[i][j]` tells the program to dereference the `char*` at position `[i][j]` and produce only the character at that index.  In the current example, the `char* charPointer` is initially set to point to the first character in the indexed string of the array.  Instead of dereferencing the `char*` using `argv[][]`, the character pointer is dereferenced using the symbol `*` before the variable name `charPointer`.  Since `charPointer` is a pointer, it is possible to use pointer aritmetic to iterate through each character in the string.  This is achieved by incrementing the pointer the same way an integer is incremented, using the unary operator `++`.  This is equivalent to incrementing `j` by one in the previous `for` loop when printing `argv[i][j]`.


###Wrapping up

For this lab, you do not need to submit anything. You should now have a working development environment, and have most of the tools you will need for the first assignment.