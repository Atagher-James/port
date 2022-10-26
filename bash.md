# Learn Bash
Bash (Bourne Again Shell) is a relatively simple coding language meant for many simple things. I like using it because there's a lot that you can do with it, but also a complexity of some things that makes it just challenging enough to want to learn it.

## How to Get Bash
 1. First, go to [Repl](https://replit.com/~) and sign in or sign up.
 2. Next, when you are logged in and on the home page, open a new Repl, select Bash, and name it whatever you want.
 3. A new Repl will open, and commands go on the left text box, and the output will go on the right. You can add or delete files and folders on the left side. For a full documentation on how Repl works, use [this](https://docs.replit.com/).
 
 `This is where single lines code will go.`
 
	This is where multiple
	lines of code will go.
 
> This is what output / message you should get, if there is one.

# Learning Bash
#### Echo Command
Firstly, let's start with the echo command. This is the basis of everything you will be doing in bash. It is used in about 80% of all of the commands! Here's an example:

`echo "Hello, World!` or `echo Hello, World!`
> Hello, World!

To get them on separate lines, just add a semicolon between echo commands:

`echo "Hello, World!"; echo "Hello, World!`

>Hello, World!
>Hello, World!

#### Declaring a Variable
Declaring a variable is simple, just use this syntax:

`Variable="String"`

But **do not** use this:

`Variable= "String"` or `Variable= 'String'`

It will return an error:

>Variable: command not found

And for the second one:
>Variable: String not found

#### Using a Variable:
You can use this

`Echo $Variable`
>String

You can use this also:

`echo "$Variable"`
>String

But **do not** use this:

`echo '$Variable'`
>$Variable

#### Parameter Extension
Parameter extensions are important because you can use them for more then one thing, not just using a declared variable.

`echo ${Variable}`
>String

Let's say we rename our variable to this:

`Variable="Very Many Strings!"`

And use this command:

`echo ${Variable/Very/A}`

This will substitute the first occurrence of "Very" with "A"
>A Many Strings

#### Lengths

This command makes it so that "Very Many Strings!" has only the first 7 characters showing:

	Length=7
	echo ${Variable:0:Length}
	
>Very Ma

This command makes it so that the last 5 characters show up:
`echo ${Variable: -5}`
>ings!

This command shows you how many characters the string is:
`echo ${#Variable}`
>18

#### Indirect Expansion
This is an expansion of a current variable:

	OtherVariable="Variable"
	echo ${!OtherVariable}

>Very Many Strings!

#### Foo
Foo is the default value for the variable if the variable declaration is empty:

`echo ${Foo:-"Default Value"}`
>Default Value

This works for null, `(Foo=0)` empty string, `(Foo="")` and zero `(Foo=0)`.

#### Arrays
Let's declare an array with 6 elements:

`array0=(one two three four five six)`

Printing the first element:

`echo $array0` or `echo ${array0[0]}`
>one

This command is to print all elements:

`echo ${array0[@]}`
>one two three four five six

This command is to print it in number form:

`echo ${#array0[@]}`
>6

This command prints all numbers in the 5th element:

`echo ${#array0[2]}`
>5

This command prints 2 elements starting from 4th:

`echo ${array0[@]:3:2}`
>four five

This command prints all elements starting on a different line:

	for i in "${array0[@]}" do
	echo "$i"
	done

>one
>two
>three
>four
>five
>six

#### Brace Expansion

These commands use ellipses to  write out the numbers 1 to 10 or the alphabet so that you don't have to write all of it out yourself.

`echo {1..10}`
> 1 2 3 4 5 6 7 8 9 10

`echo {a..z}`
> a b c d e f g h i j k l m n o p q r s t u v w x y z

Note that you **do not** have to put an `$` symbol before the curly brackets. You must have ***2*** dots between the numbers or letters.

#### Built in Variables
Here are some useful built in variables, like:

Last program's return value:

`echo $?`

Script's PID:

`echo $$`

Number of arguments passed to script:

`echo $#`

All arguments passed to script:

`echo $@`

Script's arguments separated into different variables:

`echo $1 $2 ...`

#### Listing a Directory
According to google, a directory is a file system cataloging structure which contains references to other computer files, and possibly other directories. On many computers, directories are known as folders, or drawers, analogous to a workbench or the traditional office filing cabinet.
Note: PWD means Print Working Directory.

This first command prints your working directory. The directory name is the name of the Repl. For the purposes of this lesson, let's sat that the name of the Repl is **Bash Test**.

`echo "My directory is $(pwd)` or 

`echo My directory is $PWD`
>My directory is /home/runner/Bash-Test

#### Clear Command
If your terminal has too much stuff in it, you can just type clear at the end of your script, and the terminal will clear after whatever scripts you write appear and are done. Note that if clear does not go at the end, then whatever scripts come after clear will stay in the terminal.
Command:
`clear`
> *Nothing Here*

Alternatively, you can just press Ctrl/Cmd L to clear the terminal when your Repl is not running.

#### Reading a Value from an Input
This command makes it so that you can ask the user a question.
```bash
	echo "What's your Name?"
	read Name
	echo "Hello, $Name."
```
Note that you didn't have to declare a variable, just make sure that whatever word comes after the `read` command is spelled and capitalized the exact same as what's after the `echo` command.

>What's your name?
>(User Input): John
>Hello, John.

#### If..Then Statements

Let's say we created a variable that made $USER = John.
`USER="John"`
Then we can create an if..then statement that makes the computer ask itself if the name the user puts in is the same as the username.

	if [ $Name != $USER ]
	then
	echo "I'm sorry, your name is not your username."
	else
	echo "Your name is your username!"
	fi

>What's your name?

>John

>Hello, John.

>Your name is your username!

If the name is not john, then:
>What's your name?

>Jane

>Hello, Jane.

>I'm sorry, your name is not your username.

Note: if `$Name` is empty, then, bash sees this as

`if [ != $USER ]`

This is incorrect syntax, so this is how to fix this:

`if [ "SName" != $USER ]`

So then bash sees that line, if `$Name` is empty, as:

`if [ "" != $USER ]`

This is the correct syntax.

#### Conditional Execution
Conditional execution uses phrases like `||` and `&&` as "or" and "and" to specify, for example, if this **or** this happened, then execute the command, and **only if** this **and** this happens, then the command gets executed.

	echo "Always executed" || echo "Only executed if first command fails"
	
>Always Executed

	echo "Always executed" && echo "Only executed if first command does NOT fail"

>Always Executed
>Only executed if first command does NOT fail.

Note: to use "or" and "and" statements, you need multiple sets of square brackets.

First we need to set up some read and echo commands:

	echo "What's your name?"
	read name
	echo "What's your age?"
	read age
	Your name is $name and you are $old years old.

Here is an example of using an "and" parameter:

	if [ "$name" == "John" ] && [ "$age" == -eq 15 ]"
	then
	echo "This will run if the name is John and the age is 15."
	fi

>What's your name?

>John

>What's your age?

>15

>Your name is John and you are 15 years old.

>This will run if the name is John and the age is 15.

This next one does not need the age bracket.
This is an example of using an "or" parameter:

	if [ "$name" == "John" ] || [ "$name" == "Jane" ]
	then
		echo "This will run if your name is John OR Jane"
	fi

> What's your name?

> Jane (or John)

> How old are you?

> 87

> Your name in Jane (or John) and you are 87 years old.

> This will run if your name is John OR Jane.

#### Regex Pattern
For those who don't know, the Regex pattern is a pattern that you put into the computer that a string has to follow otherwise it is invalid. The best example is an email. Let's create a variable as Email and Regex pattern:

	Email=you@example.com
	if [[ "$Email" =~ [a-z]+@[a-z]{2,}\.(com|net|org) ]]
	then
		echo "Valid Email!!
	fi

>Valid Email

Please note that the Regex pattern only works using `=~` within **double** square brackets. `[[ PARAMS ]]`
See [this](https://www.gnu.org/software/bash/manual/bashref.html#Conditional-Constructs) for more on Regex patterns and Conditional Constructs.

#### Ping
Use the command alias to send only 5 packets:

`alias ping="ping -c 5"`

Escape the alias:

Note: This one **does not** work in Repl.

`\ping 192.168.1.1`

Print all Aliases

`alias -p`

#### Math
Math is simple. Use `+` for adding, `-` sor subtracting, `*` for multiplying, and `/` for dividing. Make sure to use double parentheses.

`echo $(( 10 + 5 ))`
>15

`echo $(( 10 - 5 ))`
>5

`echo $(( 10 * 5 ))`
>50

`echo $(( 10 / 5 ))`
>2

`echo $(( 10 + 5 - 8 * 7 / 6 ))`
>8

Bash math **does not** follow order of operations, it just does the math left to right.

#### Other Files
There are many things that you can do to other files. Before I get into anything about other files, I want you to [create a text file](https://docs.replit.com/getting-started/creating-files), and name it `file.txt`. Inside of **file.txt**, I want you to type or copy/paste this sentence once: 

	The quick brown fox jumps over the lazy dog.

Let's get started with some code. Firstly, this command will list all of the directories inside of the Repl:

`ls`
> `main.sh` file.txt

This command will list all of the directories on a different line:
`ls -l`
>total 4
>-rw-r--r-- 1 runner runner 5 (month, date, time) `main.sh`
>-rw-r--r-- 1 runner runner 0 (month, date, time) file.txt

This command sorts the directory by last modified date:

`ls-t`
>`main.sh`
>file.txt

or 
>file.txt
>`main.sh`

This command will recursively `ls` this directory and all of it's subdirectories:

`ls -R`

Note: Make sure the "R" is capitalized.
>.:
>`main.sh` file.txt

This command will list all txt  files **only**.

`ls -l | grep "\.txt"`
>-rw-r--r-- 1 runner runner 1 (month day time) file.txt

This command makes it so that you can read the contents of other files without having to click on that file and see what's in that file.

`cat file.txt`
>The quick brown fox jumps over the lazy dog.

This command makes it easier to see what's in a file, if you have many of them that you're using the `cat` command on.

`Contents=$(cat file.txt)`

Note: `\n` means the next text will be printed on a new line.

Note: `-e` to interpret the newline escape characters as escape characters.

`echo -e"START OF FILE\n$Contents\nEND OF FILE"`

>START OF FILE

>The quick brown fox jumps over the lazy dog.

>END OF FILE

#### Renaming and Moving Files
These commands make it so that you can rename, add, delete, and clone directories and files right from bash.
This command clones `file.txt` and names the new file `clone.txt`.

	cp file.txt clone.txt
	ls

>`main.sh` file.txt clone.txt

This next command moves the contents of a file to another one with a different name and deletes the source one. This literally means just renaming the file.

	mv file.txt main.txt
	ls

>`main.sh`
>main.txt

#### CD Commands
These commands just change, clone, and add directories, as well as move to different directories.
These commands move you to the home directory:

`cd ~` or `cd`

This command moves up one directory:

`cd ..`

This command moves you to the last directory:

`cd -`

These commands move you to specific directories:

`cd /home/username/documents` or `cd ~/Documents/`

#### Subdirectories
Subdirectories are directories in which you can hold other information under current directories. Example:
This command uses subshells to work across directories:

	mkdir someDir
	(echo "First, I'm here: $PWD") && (cd someDir; echo "Then, I'm here: $PWD")
	
>First, I'm here: /home/runner/Bash-Test
>Then, I'm here: /home/runner/Bash-Test/someDir

This command makes a new directory:
`mkdir`
Example of this being used:

	mkdir oneDir
	cd oneDir
	echo I'm in this directory: $PWD

>I'm in this directory: /home/runner/Bash-Test/oneDir

This command will create directories as needed:

`mkdir -p myNewDir/with/intermediate/directories`

You can see all of the directories in your files section.

#### Redirecting
Redirecting puts various messages, like errors, in directories so that you can easily go through them. Take this python code for example:

	cat > hello.py << EOF
	from __future__ import print_function
	import sys
	print("#stdout", file=sys.stdout)
	print("#stderr", file=sys.stderr)
	for line in sys.stdin:
		print(line, file=sys.stdout)
	EOF

You can redirect command input and output (stdin, stdout, and stderr). Read from stdin until `^EOF$` and overwrite `hello.py` with the lines between "EOF."
There are various commands that you can use here.

Pass `input.in` as input to the script

`python hello.py < "input.in"`

Redirect output from the script to output.out:

`python hello.py > "output.out"`

Redirect error output to error.err:

`python hello.py 2> "error.err"`

Redirect both output and errors to output-and-error.log:

`python hello.py > "output-and-error.log" 2>&1`

Redirect all errors to the "black hole (/dev/null)" or no output.

`python hello.py > /dev/null 2>&1`

The output error will rewrite the file if it exists. Use `>>` if you want to append.

`python hello.py >> "output.out" 2>> "error.err"`

Overwrite output.out, append to error.err, and count lines:

	info bash 'Basic Shell Features' 'Redirections' > output.out 2>> error.err
	wc -l output.out error.err

Run a command and print it's file descriptor. (Example: /dev/fd/123)

`echo <(echo "#helloworld")`

Overwrite output.out with `#helloworld`:

	cat > output.out <(echo "#helloworld")
	echo "#helloworld" > output.out
	echo "#helloworld" | cat > output.out
	echo "#helloworld" | tee output.out >/dev/null

Cleaning up temporary files:
*Warning: The command RM cannot be undone!*

	rm -v output.out error.err output-and-error.log
	rm -r tempDir/

This recursively deletes all of it.

#### Substituting Commands
Substituting commands means that you use parentheses to substitute commands with other commands using `$( )`.

This command displays the number of files in the current directory:

`echo "There are $(ls | wc -l) items here."`
>There are 2 items here

You *can* use backticks, but that cannot be nested, so the preferred method is using `$( )`.

Bash uses a case statement that works similarly to switch in Java and C++.

	case "$Variable" in
	    # List patterns for the conditions you want to meet
	    0) echo "There is a zero.";;
	    1) echo "There is a one.";;
	    *) echo "It is not null.";;  # match everything
	esac

#### Loops
For loops itearate for as many arguments given.
The contents of `$Variable` is printed 3 times.

	for Variable in {1..3}
	do
		echo "$Variable"
	done
>1
>2
>3

This is using the traditional "for" loop way:

	for ((a=1; a <= 3; a++))
	do
	    echo $a
	done

>1
>2
>3

They can also be used to act on files.
This will run the command `cat` on `file1` and `file2`:

	for Variable in file1 file2
	do
	    cat "$Variable"
	done

This can *also* be used from an output from a command.
This will `cat` the output from `ls`.

	for Output in $(ls)
	do
	    cat "$Output"
	done

Bash can also do patterns, like this to `cat` all of the markdown files in the current directory. Create 3 markdown files and name them whatever you want so that this command will work. I named mine "a," "b," and "c."

	for Output in ./*.markdown
	do
	    cat "$Output"
	done

While Loop:

	while [ true ]
	do
	    echo "loop body here..."
	    break
	done

>Loop body here...

You can also define functions:

	{
	    echo "Arguments work just like script arguments: $@"
	    echo "And: $1  $2..."
	    echo "This is a function"
	    return 0
	}

Call the function `foo` with 2 arguments, "arg1" and "arg2"

`foo arg1 arg2`

>Arguments work just like script arguments: arg1 arg2

>And: arg1 arg2..

>This is a function

Or simply:

	bar ()
	{
	    echo "Another way to declare functions!"
	    return 0
	}

Call the function `bar` with no arguments.

`bar`
>Another way to declare functions!

Calling your function:

`foo "My name is" $Name`

#### Useful Commands to Know

Prints last 10 lines of file.txt:

`tail -n 10 file.txt`

Prints first 10 lines of file.txt:

`head -n 10 file.txt`

Sort file.txt's lines:

`sort file.txt`

Report or omit any repeated lines:

`uniq -d file.txt`

Prints only the first column before the `'` character:

`cit -d ',' -f 1 file.txt`

Replaces every occurrence of "quick" with "fast" in file.txt:

`sed -i 's/quick/fast/g' file.txt`

Print to stdout all lines of file.txt which match some regex. This example prints lines which start in "foo" and end in "bar."

`grep "^foo.*bar$" file.txt`

Use the option `-c` to instead print the number of lines that matches the regex:

`grep -c "^foo.*bar$" file.txt`

This option recursively greps the regex:

`grep -r "^foo.*bar" someDir`

This gives the line numbers that matches the regex:

`grep -n "^foo.*bar$" file.txt`

This also recursively greps the regex but ignores binary:

`grep -rI "^foo.*bar$" someDir`

Perform the same initial search, but filter out the lines
 containing "razzi."

`grep "^foo.*bar$" file.txt | grep -v "razzi"`

The `trap` command allows you to execute a command whenever your script receives a signal. Here, `trap` will execute `rm` if it receives any of the three listed signals:

`trap "rm $TEMP_FILE; exit" SIGHUP SIGINT SIGTERM`

`Sudo` is used to perform commands as the superuser:

	NAME1=$(whoami)
	NAME2=$(sudo whoami)
	echo "Was $NAME1, then became more powerful $NAME2"

#### How to get Help if Needed
In Repl there's an option, on the right where you've been using the "console" tab, there's another tab where only these following commands will work, but they can give you all the help that you need. This is the "shell" tab. if you ever need any help, just click on that and put in any of these following commands:

`help`

`help help`

`help for`

`help return`

`help source`

`help .`

Read Bash manpage documentation:

`apropos bash`

`man 1 bash`

`man bash`

Read info documentation:

`apropos info` or `grep '^info.*('` <-- This one for Console.

`man info`

`info info`

`info 5 info`

Read Bash info documentation:

`info bash`

`info bash 'Bash Features'`

`info bash 6`

`info --apropos bash`

# Thank you so Much!
If you have actually read through this, then I thank you so much! This took me about 12 total hours to complete, and if there are any mistakes, then please don't hesitate to email me at:
`26grogab@elmbrookstudents.org`. I want to disclaim so people don't yell at me in the comments: ***This is not my tutorial, I just put this into markdown and made it a little bit easier for people to understand.*** You can find the original tutorial [here](https://learnxinyminutes.com/docs/bash/). I created all of this markdown in [Stackedit](https://stackedit.io/). Again, thank you so much for reading all of this!