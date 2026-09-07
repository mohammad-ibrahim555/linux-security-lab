# Linux Processes and Services

## Overview

A **process** is a program that is currently running on a Linux system.

For example, when you open a terminal, run a command, or start an application, Linux creates a process to run it.

A **service** is a program that usually runs in the background and provides a function for the system or other programs.

Understanding processes and services is important in cybersecurity because security analysts need to know what is running on a system and identify unusual or suspicious activity.

## Beginner Safety Notes

Before practicing these commands, keep these rules in mind:

* Practice on your own Linux system, virtual machine, or authorized lab.
* Do not stop or modify processes or services on a computer you do not own or have permission to manage.
* Be careful with `kill`, `systemctl stop`, `systemctl restart`, and similar commands because they can interrupt programs or system functions.
* Always check the PID before using `kill`.
* Always check the service name and status before changing a service.
* Avoid running commands with `sudo` unless you understand what the command does.
* Do not experiment on production, school, work, or other people's systems without explicit permission.
* When learning cybersecurity, use isolated practice environments whenever possible.

## What Is a Process?

A process is a running instance of a program.

For example, when you run:

```bash
ping google.com
```

Linux creates a process to run the `ping` command.

Each process has a unique number called a **Process ID (PID)**.

Example:

```text
PID
1254
```

The PID allows Linux to identify and manage the process.

## Process ID (PID)

Every running process has a PID.

You can see process IDs using:

```bash
ps
```

Example:

```text
PID TTY          TIME CMD
1254 pts/0    00:00:00 bash
1382 pts/0    00:00:00 ps
```

In this example:

* `1254` is the PID of the `bash` process.
* `1382` is the PID of the `ps` command.

PIDs are useful when you need to identify a specific process.

## ps

The `ps` command displays information about running processes.

A basic example is:

```bash
ps
```

To see more processes, you can use:

```bash
ps aux
```

This provides more detailed information about processes running on the system.

Useful information can include:

* User running the process
* PID
* CPU usage
* Memory usage
* Start time
* Command being executed

## top

The `top` command provides a live view of running processes.

```bash
top
```

It can show:

* Running processes
* CPU usage
* Memory usage
* Process IDs
* Users
* System resource usage

This can help you understand what is using system resources.

Press:

```text
q
```

to exit `top`.

## kill

The `kill` command sends a signal to a process.

For example:

```bash
kill 1254
```

This sends a signal to the process with PID `1254`.

### Safety Warning

**Be careful with `kill`.**

Do not randomly choose a PID. Stopping the wrong process can interrupt an application or important system function.

Before using `kill`:

1. Identify the PID.
2. Check what program the PID belongs to.
3. Make sure it is a process you are allowed to control.
4. Only then send a signal.

For beginner practice, use a harmless process that you started yourself.

## Processes in the Background

Linux can run processes in the background.

For example:

```bash
sleep 60 &
```

The `&` tells the shell to run the command in the background.

You can then continue using the terminal while the command runs.

You can view background jobs with:

```bash
jobs
```

## Foreground and Background

A **foreground process** uses the terminal directly.

For example:

```bash
ping google.com
```

The command continues running in the terminal.

A **background process** runs without taking control of the terminal.

For example:

```bash
ping google.com &
```

The terminal can then be used for other commands.

## What Is a Service?

A service is a program that runs in the background and performs a specific function.

Examples can include:

* Web servers
* SSH servers
* Database servers
* Network services
* Logging services

Services are often started automatically when Linux boots.

## Process vs Service

A process and a service are related but not exactly the same.

### Process

A process is a running instance of a program.

Example:

```text
PID 1254 → bash
```

### Service

A service is a background program designed to provide a specific function.

Example:

```text
SSH service → allows remote connections
```

A service normally has one or more processes running behind it.

## systemctl

`systemctl` is used to manage services on Linux systems that use `systemd`.

You can check the status of a service with:

```bash
systemctl status service_name
```

For example:

```bash
systemctl status ssh
```

This shows information about the SSH service.

## Starting a Service

A service can be started using:

```bash
sudo systemctl start service_name
```

Example:

```bash
sudo systemctl start ssh
```

### Safety Warning

Starting a service can change how your system behaves and may make a network service available.

Only start services on systems you own or are authorized to administer.

For learning, it is safer to practice in a virtual machine or dedicated lab.

## Stopping a Service

A service can be stopped using:

```bash
sudo systemctl stop service_name
```

Example:

```bash
sudo systemctl stop ssh
```

### Safety Warning

Stopping a service can interrupt important system functionality.

Do not stop a service simply because you do not recognize its name. First find out what the service does and whether the system depends on it.

## Restarting a Service

A service can be restarted using:

```bash
sudo systemctl restart service_name
```

Example:

```bash
sudo systemctl restart ssh
```

### Safety Warning

Restarting a service temporarily interrupts that service.

Before restarting one, make sure you understand what it does and that restarting it will not disrupt something important.

## Checking Whether a Service Is Running

You can use:

```bash
systemctl is-active service_name
```

Example:

```bash
systemctl is-active ssh
```

The result may indicate whether the service is currently active.

Checking status is generally safer than changing a service because it does not modify or stop the service.

## Enabling and Disabling Services

A service can be configured to start automatically when the system boots.

To enable a service:

```bash
sudo systemctl enable service_name
```

To disable automatic startup:

```bash
sudo systemctl disable service_name
```

### Safety Warning

Enabling or disabling a service changes system startup behavior.

Do not change startup settings on a system unless you understand the service and have permission to administer the system.

## Why Processes Matter in Cybersecurity

Security professionals need to understand running processes because suspicious activity can sometimes appear as an unusual process.

For example, an analyst might investigate:

* An unknown process
* A process using unusually high CPU
* A process running under an unexpected user
* A process started from an unusual location
* Multiple unexpected processes

Commands such as:

```bash
ps aux
```

and:

```bash
top
```

can help with basic investigation.

## Why Services Matter in Cybersecurity

Services can provide important system functionality, but unnecessary or incorrectly configured services can increase the system's attack surface.

Security professionals may check:

* Which services are running
* Which services start automatically
* Which user runs a service
* Whether a service is expected
* Whether a service is properly configured

For example:

```bash
systemctl --type=service
```

can be used on systems using `systemd` to view services.

## Basic Process Investigation

A simple process investigation might look like this:

### Step 1: View running processes

```bash
ps aux
```

### Step 2: Look for a specific process

```bash
ps aux | grep ssh
```

The `|` is called a **pipe**. It sends the output of `ps aux` to `grep`.

### Step 3: Check system resource usage

```bash
top
```

### Step 4: Investigate a specific PID

Once you identify a process ID, you can gather more information about that process using appropriate Linux tools.

The goal is to understand:

```text
What is running?
Who is running it?
What resources is it using?
Is it expected?
```

## Basic Service Investigation

You can check a service with:

```bash
systemctl status service_name
```

For example:

```bash
systemctl status ssh
```

You can investigate:

* Whether the service is running
* Whether it started successfully
* Recent service messages
* The service's current state

## Useful Commands

| Command             | Purpose                                |
| ------------------- | -------------------------------------- |
| `ps`                | View running processes                 |
| `ps aux`            | View detailed process information      |
| `top`               | Monitor processes and system resources |
| `kill`              | Send a signal to a process             |
| `jobs`              | View background jobs                   |
| `systemctl status`  | Check a service's status               |
| `systemctl start`   | Start a service                        |
| `systemctl stop`    | Stop a service                         |
| `systemctl restart` | Restart a service                      |
| `systemctl enable`  | Enable automatic service startup       |
| `systemctl disable` | Disable automatic service startup      |

## Important Concepts

### Process

A running instance of a program.

### PID

A unique number assigned to a process.

### Service

A background program that provides a specific function.

### systemd

A system and service manager used by many modern Linux distributions.

### systemctl

A command used to communicate with and manage `systemd` services.

## Cybersecurity Relevance

Understanding processes and services helps security professionals monitor Linux systems and investigate unusual activity.

These skills are useful for:

* System monitoring
* Incident investigation
* Threat detection
* Troubleshooting
* Identifying unexpected software
* Understanding system behavior
* Security hardening

## Summary

A process is a program that is currently running on a Linux system.

Each process has a unique Process ID (PID).

The `ps` and `top` commands help you view and monitor processes, while `kill` can send signals to processes.

Services are background programs that provide specific functions. On systems using `systemd`, `systemctl` is used to manage services.

Always practice these commands on systems you own or are authorized to manage. When experimenting with commands that stop, restart, or modify processes and services, use a dedicated Linux lab or virtual machine whenever possible.

Understanding processes and services is an important foundation for Linux system administration and cybersecurity.
