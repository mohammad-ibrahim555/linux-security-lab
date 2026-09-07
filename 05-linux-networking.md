# Linux Networking

## Overview

Networking allows computers and other devices to communicate with each other.

In cybersecurity, understanding networking is essential because security professionals need to understand how devices communicate, how network connections work, and how to identify unusual network activity.

Linux provides several commands for viewing and troubleshooting network information.

## Beginner Safety Notes

Before practicing networking commands, keep these rules in mind:

* Practice on your own computer, virtual machine, or an authorized lab.
* Do not scan, probe, or test systems that you do not own or have permission to test.
* Network information can be sensitive, so do not publicly share private IP addresses, usernames, or other system details unnecessarily.
* Commands such as `ping`, `curl`, and `traceroute` send network traffic to other systems.
* Only use these commands against destinations you are allowed to contact.
* Be careful when downloading files with `wget` or retrieving content with `curl`.
* Do not download or run unknown files.
* Use a virtual machine or dedicated lab when practicing cybersecurity networking skills.

## What Is a Network?

A network is a group of connected devices that can communicate with each other.

Examples include:

* Computers
* Phones
* Servers
* Routers
* Network printers
* Virtual machines

The internet is a very large network made up of many connected networks.

## IP Addresses

An IP address identifies a device or network interface on a network.

An IPv4 address looks like:

```text
192.168.1.10
```

IPv4 addresses contain four numbers separated by periods.

Another version is IPv6.

An IPv6 address can look like:

```text
2001:db8::1
```

IPv6 was developed to provide a much larger number of available addresses.

## Private and Public IP Addresses

A **private IP address** is normally used inside a local network.

Common private IPv4 ranges include:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

For example:

```text
192.168.1.10
```

A **public IP address** is used for communication across the public internet.

Your home network may use private IP addresses internally while your router communicates with the internet using a public IP address.

## Network Interfaces

A network interface is the part of a computer that allows it to communicate over a network.

Examples include:

* Ethernet
* Wi-Fi
* Virtual network interfaces

Linux provides the `ip` command for viewing network information.

## ip

The `ip` command can display and manage network configuration.

To view network interfaces and their addresses:

```bash
ip addr
```

You may also see:

```bash
ip a
```

These commands can show:

* Network interfaces
* IP addresses
* Interface status
* MAC addresses
* IPv4 information
* IPv6 information

## Viewing Network Interfaces

You can use:

```bash
ip link
```

This displays information about network interfaces.

For example, you may see interfaces such as:

```text
lo
eth0
wlan0
```

The exact names depend on the Linux system.

### The loopback interface

The `lo` interface is the loopback interface.

It allows the computer to communicate with itself.

The common loopback IPv4 address is:

```text
127.0.0.1
```

This is often called **localhost**.

## ping

The `ping` command checks whether a destination responds to network requests.

Example:

```bash
ping example.com
```

On many Linux systems, `ping` continues until you stop it.

Press:

```text
Ctrl + C
```

to stop the command.

You can also specify a number of requests:

```bash
ping -c 4 example.com
```

This sends four requests.

## Understanding ping Results

A successful `ping` may show information such as:

```text
64 bytes from ...
time=20 ms
```

The response time gives an indication of how long the network request took.

If there is no response, it does **not necessarily mean the destination is offline**.

A system or firewall may simply be configured not to respond to ping requests.

## Safety Note for ping

`ping` sends traffic to another system.

For normal learning, use:

* Your own computer
* Your own virtual machines
* Systems you are authorized to test

Avoid repeatedly sending large amounts of traffic to systems you do not control.

## ss

The `ss` command displays network connections and listening sockets.

For example:

```bash
ss
```

You can view listening TCP and UDP sockets with:

```bash
ss -tuln
```

This can help you understand which network services are listening for connections.

Useful options include:

```text
-t = TCP
-u = UDP
-l = listening
-n = show numerical addresses and ports
```

## Ports

A port helps identify a particular network service on a device.

Port numbers range from:

```text
0 - 65535
```

Some commonly encountered ports include:

| Port | Common use |
| ---: | ---------- |
|   22 | SSH        |
|   53 | DNS        |
|   80 | HTTP       |
|  443 | HTTPS      |

These are common associations, but the actual service using a port depends on the system's configuration.

## TCP and UDP

TCP and UDP are two important transport-layer protocols.

### TCP

TCP provides reliable, connection-oriented communication.

It is commonly used when data needs to arrive reliably and in order.

### UDP

UDP is connectionless and has less overhead than TCP.

It can be useful when speed and low overhead are more important than guaranteed delivery.

## curl

The `curl` command can communicate with URLs and transfer data.

For example:

```bash
curl https://example.com
```

This can retrieve the response from a web server.

You can also use:

```bash
curl -I https://example.com
```

to request response headers.

Headers can provide information about the server's HTTP response.

## Safety Note for curl

Be careful when using `curl` with unknown websites or URLs.

`curl` retrieves data but does not automatically make downloaded content safe.

Do not execute commands or scripts simply because they were returned by a website.

For learning, use trusted websites or your own lab environment.

## wget

The `wget` command is commonly used to download files from URLs.

Example:

```bash
wget https://example.com/file.txt
```

This downloads the specified file.

## Safety Note for wget

Only download files from sources you trust or are authorized to use.

Downloading a file does not mean the file is safe.

Do not run unknown downloaded programs or scripts.

## traceroute

The `traceroute` command shows the network path that packets take toward a destination.

Example:

```bash
traceroute example.com
```

Some Linux systems may require:

```bash
sudo traceroute example.com
```

or may use a different tool such as:

```bash
tracepath example.com
```

The output can show multiple network hops between your computer and the destination.

## Understanding Network Hops

A **hop** is a step through a network device or router along the path to a destination.

A simplified path might look like:

```text
Your computer
     ↓
Home router
     ↓
Internet router
     ↓
Another router
     ↓
Destination
```

The actual path can be much more complicated.

Network paths can also change over time.

## DNS

DNS stands for **Domain Name System**.

DNS translates domain names into IP addresses.

For example:

```text
example.com
```

can be associated with an IP address.

This allows people to use domain names instead of remembering numerical IP addresses.

You can use:

```bash
ping example.com
```

to see the address that the system resolves for the domain.

## Basic Network Troubleshooting

When a network connection does not work, you can investigate it step by step.

### Step 1: Check network interfaces

```bash
ip addr
```

Look for an interface with an IP address.

### Step 2: Test connectivity

```bash
ping -c 4 example.com
```

This tests whether the destination responds.

### Step 3: Check network connections

```bash
ss -tuln
```

This shows listening TCP and UDP sockets.

### Step 4: Check the network path

```bash
traceroute example.com
```

This can help identify where problems may occur along the network path.

The goal is to understand:

```text
Do I have a network connection?
        ↓
Can I reach the destination?
        ↓
Are network services listening?
        ↓
Where might the connection be failing?
```

## Network Information and Cybersecurity

Networking knowledge is important for cybersecurity because computers constantly communicate with other systems.

Security professionals may need to understand:

* IP addresses
* Network interfaces
* Ports
* Network connections
* Protocols
* DNS
* Network paths
* Listening services

This information can help analysts understand normal system behavior and investigate unusual activity.

## Network Connections and Security

The `ss` command can help identify listening services and network connections.

For example:

```bash
ss -tuln
```

An analyst may ask:

```text
Which ports are listening?
Which services are using them?
Are these services expected?
```

Unexpected listening services may require further investigation.

## Common Networking Commands

| Command      | Purpose                                |
| ------------ | -------------------------------------- |
| `ip addr`    | View IP addresses and interfaces       |
| `ip link`    | View network interfaces                |
| `ping`       | Test network reachability              |
| `ss`         | View network connections and sockets   |
| `curl`       | Communicate with URLs                  |
| `wget`       | Download files                         |
| `traceroute` | View the network path to a destination |

## Quick Reference

### IP information

```bash
ip addr
```

### Network interfaces

```bash
ip link
```

### Test connectivity

```bash
ping -c 4 example.com
```

### View listening sockets

```bash
ss -tuln
```

### Access a website

```bash
curl https://example.com
```

### Download a file

```bash
wget https://example.com/file.txt
```

### View network path

```bash
traceroute example.com
```

## Important Concepts

### IP Address

An address used to identify a device or network interface.

### Port

A number used to identify a network service or endpoint.

### Network Interface

A hardware or virtual interface used for network communication.

### TCP

A reliable, connection-oriented transport protocol.

### UDP

A connectionless transport protocol with lower overhead.

### DNS

A system that translates domain names into IP addresses.

### Network Hop

A step through a network device or router along a network path.

## Cybersecurity Relevance

Linux networking skills are useful for:

* Network troubleshooting
* Security monitoring
* Incident investigation
* Understanding network connections
* Identifying listening services
* Understanding how systems communicate
* Analyzing network-related security events

Networking is one of the most important foundations for cybersecurity because many security events involve communication between systems.

## Summary

Linux provides several commands for understanding and troubleshooting networks.

The `ip` command helps view network interfaces and IP addresses.

The `ping` command can test network reachability.

The `ss` command helps identify network connections and listening sockets.

`curl` and `wget` can communicate with websites and transfer data, while `traceroute` can show the path toward a destination.

Understanding IP addresses, ports, protocols, DNS, and network connections provides an important foundation for cybersecurity.

Always practice networking commands on systems and networks you own or are authorized to test.
