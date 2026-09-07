# Linux File Management

## Overview

Linux provides commands for creating, viewing, searching, copying, moving, and removing files and directories.

Understanding file management is important in cybersecurity because security analysts often need to locate files, examine their contents, organize data, and investigate a Linux system.

## Creating Directories

### mkdir

The `mkdir` command creates a new directory.

### Syntax

```bash
mkdir directory_name
```

### Example

```bash
mkdir security-notes
```

This creates a directory called `security-notes`.

## Creating Files

### touch

The `touch` command can create a new empty file.

### Syntax

```bash
touch filename
```

### Example

```bash
touch notes.txt
```

This creates an empty file called `notes.txt`.

## Copying Files

### cp

The `cp` command copies a file or directory.

### Syntax

```bash
cp source destination
```

### Example

```bash
cp notes.txt backup.txt
```

This creates a copy of `notes.txt` called `backup.txt`.

## Moving and Renaming Files

### mv

The `mv` command can move a file or directory to another location. It can also be used to rename a file.

### Move a file

```bash
mv notes.txt Documents/
```

This moves `notes.txt` into the `Documents` directory.

### Rename a file

```bash
mv notes.txt linux-notes.txt
```

This renames `notes.txt` to `linux-notes.txt`.

## Removing Files

### rm

The `rm` command removes files.

### Syntax

```bash
rm filename
```

### Example

```bash
rm notes.txt
```

This removes `notes.txt`.

Be careful when using `rm` because deleted files may not be recoverable through a normal undo operation.

## Viewing File Contents

### cat

The `cat` command displays the contents of a file.

### Example

```bash
cat notes.txt
```

This displays the contents of `notes.txt` in the terminal.

### less

The `less` command allows you to view a file one screen at a time.

### Example

```bash
less notes.txt
```

This is useful for reading large files without displaying everything at once.

Press `q` to exit `less`.

## Viewing the Beginning of a File

### head

The `head` command displays the beginning of a file.

By default, it displays the first 10 lines.

### Example

```bash
head notes.txt
```

You can specify the number of lines:

```bash
head -n 5 notes.txt
```

This displays the first 5 lines.

## Viewing the End of a File

### tail

The `tail` command displays the end of a file.

By default, it displays the last 10 lines.

### Example

```bash
tail notes.txt
```

You can specify the number of lines:

```bash
tail -n 5 notes.txt
```

This displays the last 5 lines.

## Finding Files and Directories

### find

The `find` command searches for files and directories.

### Example

```bash
find . -name "notes.txt"
```

The `.` means to search from the current directory.

The command searches for a file named `notes.txt`.

## Searching Inside Files

### grep

The `grep` command searches for matching text inside files.

### Example

```bash
grep "password" notes.txt
```

This searches `notes.txt` for lines containing the word `password`.

In cybersecurity, `grep` can be useful when searching logs and configuration files for specific information.

## Basic File Management Workflow

A simple Linux file-management workflow might look like this:

```bash
mkdir security-lab
cd security-lab
touch notes.txt
cat notes.txt
cp notes.txt backup.txt
mv backup.txt backup-notes.txt
ls
```

This workflow:

1. Creates a directory.
2. Enters the directory.
3. Creates a file.
4. Displays the file contents.
5. Copies the file.
6. Renames the copy.
7. Lists the files.

## Cybersecurity Relevance

File management is an important Linux skill for cybersecurity.

Security professionals may need to:

* Locate files during investigations
* Examine log files
* Search files for specific information
* Create and organize notes or scripts
* Copy files for analysis or backup
* Identify suspicious files and directories
* Understand where important system files are stored

## Commands Covered

| Command | Purpose                          |
| ------- | -------------------------------- |
| `mkdir` | Create directories               |
| `touch` | Create empty files               |
| `cp`    | Copy files or directories        |
| `mv`    | Move or rename files             |
| `rm`    | Remove files or directories      |
| `cat`   | Display file contents            |
| `less`  | View files one screen at a time  |
| `head`  | View the beginning of a file     |
| `tail`  | View the end of a file           |
| `find`  | Search for files and directories |
| `grep`  | Search for text inside files     |
