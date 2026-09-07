# Linux Permissions and Users

## Overview

Linux uses users, groups, ownership, and permissions to control who can access files and directories.

Understanding permissions is important in cybersecurity because incorrect permissions can allow users or programs to access files they should not be able to access.

## Users

A Linux system can have multiple users.

Each user has their own account and permissions.

For example:

```text
alice
bob
admin
```

A user may be allowed to read, write, or execute certain files depending on their permissions.

## Groups

Groups allow multiple users to share the same permissions.

For example, a system could have a group called:

```text
developers
```

Several users can belong to this group.

Instead of giving permissions to each user individually, permissions can be assigned to the group.

## File Ownership

Every file and directory in Linux has an owner and a group.

You can view ownership information using:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 alice developers 1200 notes.txt
```

In this example:

* `alice` is the owner.
* `developers` is the group.
* `notes.txt` is the file.

## Understanding Permissions

Linux permissions are divided into three categories:

```text
User     Group     Others
```

They are often shown like this:

```text
-rwxr-xr--
```

The permissions can be divided into:

```text
rwx | r-x | r--
user  group others
```

## Permission Types

There are three basic permissions:

| Permission | Symbol | Meaning                              |
| ---------- | ------ | ------------------------------------ |
| Read       | `r`    | View the contents of a file          |
| Write      | `w`    | Modify a file                        |
| Execute    | `x`    | Execute a file or access a directory |

For a file:

* `r` allows the user to read it.
* `w` allows the user to modify it.
* `x` allows the user to execute it.

## Reading Permission Strings

Consider:

```text
-rwxr-xr--
```

The first character indicates the file type.

```text
-
```

The `-` means it is a regular file.

The remaining nine characters are divided into three groups:

```text
rwx | r-x | r--
```

### User

```text
rwx
```

The owner can:

* Read
* Write
* Execute

### Group

```text
r-x
```

The group can:

* Read
* Execute

The group cannot write to the file.

### Others

```text
r--
```

Everyone else can:

* Read

They cannot write or execute the file.

## chmod

The `chmod` command changes file permissions.

### Example

```bash
chmod u+x script.sh
```

This gives the file owner permission to execute `script.sh`.

Another example:

```bash
chmod u-w notes.txt
```

This removes write permission from the file owner.

## Symbolic Permission Notation

Permissions can be changed using letters.

The main categories are:

```text
u = user
g = group
o = others
a = all
```

Permission symbols:

```text
r = read
w = write
x = execute
```

For example:

```bash
chmod g+w notes.txt
```

This gives the group write permission.

```bash
chmod o-r notes.txt
```

This removes read permission from others.

## Numeric Permissions

Linux also allows permissions to be represented using numbers.

The values are:

| Permission | Value |
| ---------- | ----: |
| Read       |     4 |
| Write      |     2 |
| Execute    |     1 |

The values are added together.

For example:

```text
Read + Write = 4 + 2 = 6
```

So:

```text
6 = rw-
```

Another example:

```text
Read + Execute = 4 + 1 = 5
```

So:

```text
5 = r-x
```

## Example: chmod 755

A common permission setting is:

```bash
chmod 755 script.sh
```

This means:

```text
7 = rwx
5 = r-x
5 = r-x
```

Therefore:

```text
rwxr-xr-x
```

The owner can read, write, and execute.

The group can read and execute.

Others can read and execute.

## chown

The `chown` command changes the owner of a file or directory.

### Example

```bash
chown alice notes.txt
```

This changes the owner of `notes.txt` to `alice`.

You can also change the owner and group:

```bash
chown alice:developers notes.txt
```

This makes:

```text
Owner: alice
Group: developers
```

Changing ownership usually requires administrator privileges.

## Viewing File Permissions

Use:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 alice developers 1200 notes.txt
```

The permission section is:

```text
-rw-r--r--
```

The owner is:

```text
alice
```

The group is:

```text
developers
```

## Why Permissions Matter in Cybersecurity

File permissions are an important part of Linux security.

Poor permissions can allow unauthorized users or programs to:

* Read sensitive files
* Modify important files
* Execute unwanted programs
* Access information they should not have access to

Security professionals need to understand permissions when investigating systems and checking whether files are properly protected.

## Example Security Scenario

Imagine a file contains sensitive information:

```text
credentials.txt
```

If the file has permissions that allow every user on the system to read it, the information may be exposed.

You can check the permissions with:

```bash
ls -l credentials.txt
```

A security analyst can then determine whether the permissions are appropriate.

## Important Principle: Least Privilege

A major cybersecurity principle is **least privilege**.

Least privilege means giving users and programs only the permissions they need to perform their tasks.

For example, if a user only needs to read a file, they should not automatically have permission to modify or execute it.

This reduces the potential impact of mistakes or compromised accounts.

## Useful Commands

| Command  | Purpose                                                 |
| -------- | ------------------------------------------------------- |
| `ls -l`  | View permissions, ownership, and other file information |
| `chmod`  | Change file permissions                                 |
| `chown`  | Change file ownership                                   |
| `whoami` | Show the current user                                   |
| `id`     | Show user and group information                         |
| `groups` | Show the groups a user belongs to                       |

## Quick Reference

```text
r = Read = 4
w = Write = 2
x = Execute = 1
```

Permission groups:

```text
u = User
g = Group
o = Others
a = All
```

Common commands:

```bash
ls -l
chmod
chown
whoami
id
groups
```

## Summary

Linux uses users, groups, ownership, and permissions to control access to files and directories.

The three main permissions are:

* Read
* Write
* Execute

The `chmod` command changes permissions, while `chown` changes ownership.

Understanding these concepts is essential for securing Linux systems and is an important foundation for cybersecurity.
