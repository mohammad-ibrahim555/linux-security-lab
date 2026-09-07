# Linux Shell and Bash

## Overview

A **shell** is a program that allows you to interact with the operating system by entering commands.

**Bash** is one of the most commonly used shells on Linux.

Instead of clicking buttons and menus, you can use Bash to give the computer instructions through text.

Bash is important in cybersecurity because security professionals often use the command line to investigate systems, automate tasks, analyze files, and work with security tools.

## Beginner Safety Notes

Before practicing Bash commands and scripts, keep these rules in mind:

* Practice on your own computer, virtual machine, or authorized lab.
* Be careful when running commands you do not understand.
* Do not copy and run random commands from the internet without understanding what they do.
* Be especially careful with commands that delete, modify, or overwrite files.
* Remember that `rm`, redirection such as `>`, and scripts can change or remove data.
* Do not run scripts on systems you do not own or have permission to manage.
* Avoid using `sudo` unless you understand why administrator privileges are required.
* When learning Bash scripting, use a dedicated practice directory or virtual machine.

## What Is a Shell?

A shell is a program that accepts commands from you and asks the operating system to perform them.

A simplified process looks like this:

```text
You
 ↓
Shell
 ↓
Operating System
 ↓
Computer performs the task
```

For example, when you type:

```bash
pwd
```

the shell processes the command and asks Linux to show your current directory.

## What Is Bash?

**Bash** stands for **Bourne Again Shell**.

It is a command-line shell commonly used on Linux systems.

Bash can:

* Run commands
* Work with files
* Create variables
* Use environment variables
* Connect commands together
* Redirect input and output
* Run scripts
* Automate repetitive tasks

## Terminal vs Shell

The **terminal** and **shell** are related but are not the same thing.

### Terminal

A terminal is the application or interface where you interact with the command line.

### Shell

The shell is the program running inside the terminal that interprets your commands.

A simple way to remember this is:

```text
Terminal = Where you type
Shell = What understands your commands
```

## Command Syntax

Command syntax describes the basic structure of a command.

A common structure is:

```text
command [options] [arguments]
```

For example:

```bash
ls -l /home
```

Here:

* `ls` is the command.
* `-l` is an option.
* `/home` is an argument.

Not every command needs options or arguments.

For example:

```bash
pwd
```

only uses the command.

Another example:

```bash
mkdir practice
```

uses:

* `mkdir` as the command
* `practice` as the argument

## Getting Help

Linux provides several ways to learn about commands.

### `--help`

Many commands support the `--help` option.

Example:

```bash
ls --help
```

This displays information about how the command can be used.

### `man`

The `man` command displays a command's manual page.

Example:

```bash
man ls
```

Manual pages contain detailed information about commands, options, and usage.

Press:

```text
q
```

to exit a manual page.

### Safety Note

Reading documentation before using an unfamiliar command is a good habit.

Understanding the options of a command can help prevent mistakes.

## Basic Bash Commands

Bash allows you to run Linux commands such as:

```bash
pwd
ls
cd
mkdir
touch
cat
```

For example:

```bash
mkdir practice
cd practice
touch notes.txt
ls
```

This creates a directory, enters it, creates a file, and lists the contents.

## echo

The `echo` command displays text in the terminal.

### Syntax

```text
echo [text]
```

### Example

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

`echo` is also commonly used when working with variables.

## Bash Variables

A variable stores a value that can be used later.

### Syntax

```text
variable="value"
```

Example:

```bash
name="Linux"
```

You can display the value using:

```bash
echo "$name"
```

Output:

```text
Linux
```

The `$` tells Bash that you want to use the value stored in the variable.

## Important Variable Rule

When assigning a variable, do not put spaces around `=`.

Correct:

```bash
name="Linux"
```

Incorrect:

```bash
name = "Linux"
```

The second example is not valid Bash variable assignment.

## Environment Variables

Environment variables are variables that provide information to programs running in the shell environment.

Examples include:

```bash
echo "$HOME"
echo "$USER"
echo "$PATH"
```

### HOME

`HOME` usually contains the path to the current user's home directory.

```bash
echo "$HOME"
```

### USER

`USER` usually contains the current username.

```bash
echo "$USER"
```

### PATH

`PATH` contains directories where the shell looks for executable commands.

You can view it with:

```bash
echo "$PATH"
```

The directories are usually separated by colons:

```text
/usr/local/bin:/usr/bin:/bin
```

## Why Environment Variables Matter

Environment variables allow programs and the shell to access configuration and system information.

In cybersecurity, environment variables can be important when investigating:

* How a program is configured
* Which user is running a process
* Where commands are being searched for
* How applications behave

Be careful when sharing terminal output because environment variables can sometimes contain sensitive information.

## Pipes

A **pipe** connects the output of one command to the input of another command.

The pipe symbol is:

```text
|
```

### Syntax

```text
command1 | command2
```

Example:

```bash
ls | grep ".txt"
```

The process works like this:

```text
ls
 ↓
output
 ↓
|
 ↓
grep
 ↓
matching results
```

The `ls` command produces output, and `grep` searches that output.

## Why Pipes Are Useful

Pipes allow you to combine simple commands to perform more useful tasks.

For example:

```bash
ps aux | grep bash
```

This displays process information and then searches the output for `bash`.

Pipes are commonly used when analyzing logs, processes, files, and system information.

## Output Redirection

Normally, a command displays its output in the terminal.

Redirection allows you to send that output somewhere else.

The `>` operator redirects output to a file.

### Syntax

```text
command > filename
```

Example:

```bash
echo "Linux notes" > notes.txt
```

This writes the text into `notes.txt`.

## Important Safety Warning: `>`

The `>` operator can **overwrite an existing file**.

For example:

```bash
echo "New text" > notes.txt
```

If `notes.txt` already contains information, its previous contents can be replaced.

Always check the filename before using `>`.

## Append with `>>`

The `>>` operator adds output to the end of a file instead of replacing its existing contents.

### Syntax

```text
command >> filename
```

Example:

```bash
echo "Another note" >> notes.txt
```

This adds the text to the end of `notes.txt`.

A simple way to remember:

```text
>  = replace
>> = add to the end
```

## Input Redirection

The `<` operator can provide input to a command from a file.

### Syntax

```text
command < filename
```

For example:

```bash
wc -l < notes.txt
```

This gives the contents of `notes.txt` as input to `wc`.

## Error Redirection

Programs can produce normal output and error messages.

Standard output is commonly represented as:

```text
stdout
```

Error output is commonly represented as:

```text
stderr
```

You can redirect error output using:

### Syntax

```text
command 2> filename
```

For example:

```bash
ls missing-file 2> errors.txt
```

The error message is written to `errors.txt`.

## Command Chaining

Bash allows commands to be connected together.

### Semicolon

A semicolon allows multiple commands to be written on one line:

```bash
pwd; ls
```

Both commands are executed.

### `&&`

The `&&` operator runs the second command only if the first command succeeds.

### Syntax

```text
command1 && command2
```

Example:

```bash
mkdir practice && cd practice
```

If `mkdir practice` succeeds, Bash runs `cd practice`.

This is useful when you want one step to depend on another.

## Exit Status

Commands usually return an exit status after they finish.

A successful command normally returns:

```text
0
```

A non-zero value generally indicates that something went wrong.

You can view the previous command's exit status with:

```bash
echo $?
```

Example:

```bash
ls
echo $?
```

If `ls` succeeds, the result will normally be:

```text
0
```

## Comments

Comments are notes in a Bash script that Bash does not execute.

A comment starts with:

```text
#
```

Example:

```bash
# Display the current directory
pwd
```

Comments make scripts easier for humans to understand.

## Bash Scripts

A Bash script is a text file containing Bash commands.

For example:

```bash
#!/bin/bash

echo "Starting Linux practice"
pwd
ls
```

A script can contain several commands that are executed in sequence.

## Creating a Bash Script

Create a file:

```bash
touch practice.sh
```

Open it with a text editor and add:

```bash
#!/bin/bash

echo "Linux practice"
pwd
ls
```

The first line:

```bash
#!/bin/bash
```

is called a **shebang**.

It tells the system which interpreter should be used to run the script.

## Running a Bash Script

One common method is:

```bash
bash practice.sh
```

This tells Bash to execute the script.

You can also make a script executable with:

```bash
chmod +x practice.sh
```

Then run it with:

```bash
./practice.sh
```

### Safety Warning

Only make scripts executable when you understand what they contain.

Before running a script, read through it and understand what each command does.

## Simple If Statements

Bash can make decisions using `if` statements.

Example:

```bash
#!/bin/bash

name="Linux"

if [ "$name" = "Linux" ]; then
    echo "The value is Linux"
fi
```

The script checks a condition.

If the condition is true, the command inside the `if` block runs.

## Simple Loops

Bash can repeat commands using loops.

Example:

```bash
for file in *.txt
do
    echo "$file"
done
```

This goes through `.txt` files in the current directory and displays their names.

Loops are useful for automating repetitive tasks.

## Basic Bash Workflow

A simple Bash workflow might look like:

```bash
mkdir bash-lab
cd bash-lab
touch notes.txt
echo "Linux practice" > notes.txt
cat notes.txt
```

This:

1. Creates a directory.
2. Enters the directory.
3. Creates a file.
4. Writes text into the file.
5. Displays the file contents.

## Cybersecurity Example

Bash can help automate simple security-related tasks.

For example, you could combine commands to inspect files:

```bash
ls -la | grep ".log"
```

This lists files and searches the output for names containing `.log`.

Bash can also be used to automate repetitive administrative and analysis tasks.

Automation can save time and reduce repetitive manual work.

## Troubleshooting Bash Commands

When a command does not work, do not immediately assume something is broken.

Use a simple troubleshooting process.

### 1. Check the command spelling

For example:

```bash
pwdd
```

will normally fail because `pwdd` is not the correct command.

Try:

```bash
pwd
```

### 2. Read the error message

Linux often provides useful information when a command fails.

For example:

```text
command not found
```

usually means the shell could not find a command with that name.

### 3. Check your current directory

Use:

```bash
pwd
```

You may be working in a different directory than expected.

### 4. List the files

Use:

```bash
ls
```

Check whether the file you are trying to access actually exists.

### 5. Check command help

Try:

```bash
command --help
```

For example:

```bash
grep --help
```

### 6. Check the manual

Use:

```bash
man command
```

For example:

```bash
man grep
```

### 7. Check permissions

If you cannot access or execute a file, check its permissions:

```bash
ls -l filename
```

### 8. Check the previous command's exit status

Use:

```bash
echo $?
```

A result of `0` normally means success.

A non-zero result usually means an error occurred.

## Common Beginner Problems

### `command not found`

Possible causes:

* Typo in the command
* Command is not installed
* Command is not available in the current `PATH`

Try:

```bash
command --help
```

or:

```bash
which command
```

### `No such file or directory`

Possible causes:

* Incorrect filename
* Incorrect path
* File does not exist
* You are in the wrong directory

Try:

```bash
pwd
ls
```

### `Permission denied`

Possible causes:

* You do not have permission to access the file.
* The file is not executable.
* The directory does not allow the required access.

Check:

```bash
ls -l filename
```

Do not automatically use `sudo` to bypass an error. First understand why the permission was denied.

### Unexpected output

If a command produces unexpected results:

1. Read the command again.
2. Check its options and arguments.
3. Check your current directory.
4. Read the command's help or manual page.
5. Try the command on a safe test file.

## Why Bash Matters in Cybersecurity

Bash is useful for:

* System administration
* Log analysis
* File investigation
* Automation
* System monitoring
* Security analysis
* Running security tools
* Repeating tasks efficiently

Many cybersecurity professionals work with Linux systems, making Bash an important practical skill.

## Useful Bash Concepts

| Concept              | Purpose                                                |
| -------------------- | ------------------------------------------------------ |
| Shell                | Interprets commands                                    |
| Bash                 | A commonly used Linux shell                            |
| Variable             | Stores a value                                         |
| Environment variable | Provides information to programs and the shell         |
| Pipe `\|`            | Sends output from one command to another               |
| `>`                  | Redirects output and can overwrite a file              |
| `>>`                 | Appends output to a file                               |
| `<`                  | Provides input from a file                             |
| `2>`                 | Redirects error output                                 |
| `&&`                 | Runs the next command if the previous command succeeds |
| `$?`                 | Shows the previous command's exit status               |
| `#`                  | Starts a comment                                       |
| Script               | A file containing commands to execute                  |

## Beginner Practice

Create a safe practice directory:

```bash
mkdir bash-practice
cd bash-practice
```

Create a file:

```bash
touch notes.txt
```

Write some text:

```bash
echo "Linux is useful for cybersecurity" > notes.txt
```

View the file:

```bash
cat notes.txt
```

Append another line:

```bash
echo "Bash can automate tasks" >> notes.txt
```

View the file again:

```bash
cat notes.txt
```

Search the output:

```bash
cat notes.txt | grep "Bash"
```

Check the exit status:

```bash
echo $?
```

This small exercise demonstrates:

* Output redirection
* Appending
* Pipes
* `grep`
* Exit status

## Important Safety Reminder

The commands in this file can modify files and execute scripts.

Before running a command, ask:

```text
What will this command do?
Which files will it affect?
Could it overwrite or delete anything?
Do I have permission to do this?
```

Developing this habit is important for both Linux administration and cybersecurity.

## Summary

A shell allows you to interact with an operating system using commands.

Bash is a commonly used Linux shell that can run commands, work with variables, connect commands together, redirect input and output, and execute scripts.

Pipes allow commands to work together, while redirection allows command output or errors to be sent to files.

Bash scripting can automate repetitive tasks and is an important skill for cybersecurity professionals working with Linux.

When a command fails, check the spelling, error message, current directory, file permissions, command documentation, and exit status before making changes.

Always understand a command or script before running it, and practice in an environment where you have permission to make changes.
