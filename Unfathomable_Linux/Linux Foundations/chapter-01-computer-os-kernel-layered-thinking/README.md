# Linux Foundations: Computer, Operating System, Kernel, and Layered Troubleshooting

## Overview

This repository documents my Linux-to-SRE learning journey, starting from the absolute foundation: understanding what a computer is, why operating systems exist, what the Linux kernel does, and how engineers troubleshoot systems using layered thinking.

The goal of this chapter is not to memorize Linux commands.
The goal is to build the mental model required to think like a Linux engineer, DevOps engineer, and site reliability engineer.

---

## Learning Objective

By the end of this chapter, I should be able to explain the following:

- What a computer does at a basic level
- The difference between hardware and software
- Why operating systems exist
- What the Linux kernel is responsible for
- Why applications cannot safely control hardware directly
- Why “VM running” does not always mean “Linux is healthy”
- How to analyze incidents using layered troubleshooting

---

## Core Concept

A computer mainly performs four activities:

```text
Input → Processing → Output
             ↓
          Storage
```

However, hardware alone is not enough.

Raw hardware does not understand:

- Files
- Directories
- Users
- Permissions
- Applications
- Services
- Networking
- Security

That is why an operating system exists.

The operating system manages hardware and provides a safe environment for applications to run.

---

## Computer System Layers

A simplified Linux-based system can be viewed like this:

```text
+------------------------------------------------+
| User Applications                              |
| browser, database, web server, editor          |
+------------------------------------------------+
| Shell / GUI / Tools                            |
| bash, terminal, system utilities               |
+------------------------------------------------+
| System Libraries                               |
| glibc, shared libraries                        |
+------------------------------------------------+
| System Calls                                   |
| open(), read(), write(), fork(), exec()        |
+------------------------------------------------+
| Linux Kernel                                   |
| process, memory, filesystem, network, drivers  |
+------------------------------------------------+
| Hardware                                       |
| CPU, RAM, disk, NIC, keyboard, screen          |
+------------------------------------------------+
```

---

## What Is the Kernel?

The kernel is the core part of the operating system.

In Linux:

```text
Linux = Kernel
Linux-based OS = Kernel + user-space tools + services + libraries + package manager
```

A usable Linux system includes:

```text
Usable Linux System
├── Linux kernel
├── GNU tools
├── Shell
├── System libraries
├── systemd/services
├── Package manager
└── Applications
```

---

## Kernel Responsibilities

| Kernel Responsibility | Meaning                                           |
| --------------------- | ------------------------------------------------- |
| CPU scheduling        | Decides which process gets CPU time               |
| Memory management     | Controls how RAM is used                          |
| Filesystems           | Manages how data is stored and accessed           |
| Device drivers        | Allows the OS to communicate with hardware        |
| Networking            | Handles packet movement and network communication |
| Security              | Enforces permissions and access rules             |
| Processes             | Manages running programs                          |

Key mental model:

```text
Programs ask. The kernel decides.
```

Applications do not directly control hardware.
They request help from the kernel through system calls.

Example:

```text
Application wants to read a file
        ↓
read() system call
        ↓
Kernel checks permissions
        ↓
Kernel talks to filesystem
        ↓
Kernel talks to disk driver
        ↓
Data returns to application
```

---

## Why Operating Systems Exist

Without an operating system:

```text
App 1 ─┐
App 2 ─┼── Directly fighting for CPU, RAM, Disk, Network
App 3 ─┘
```

With an operating system:

```text
App 1 ─┐
App 2 ─┼── Operating System ─── Hardware
App 3 ─┘
```

The operating system provides:

- Resource sharing
- Security
- Hardware abstraction
- Process management
- Filesystem management
- Networking
- Stability
- Controlled access to hardware

---

## Important SRE Lesson

A cloud dashboard may show the following:

```text
Instance status: running
```

But that does not always mean Linux is healthy.

The VM may be powered on, while Linux may be

- Stuck during boot
- In kernel panic
- Unable to mount the root filesystem
- Unable to start systemd
- Unable to start networking
- Unable to start SSH
- Unable to send monitoring metrics
- Unable to run the application

A healthy Linux system usually means the following:

```text
Kernel booted successfully
Root filesystem mounted
systemd started
Network initialized
SSH service running
Monitoring agent running
Application running
```

---

## Layered Troubleshooting Model

During incidents, the first goal is not to run random commands.

The first goal is to identify the failing layer.

```text
Cloud / VM layer
   ↓
Firmware / bootloader layer
   ↓
Kernel layer
   ↓
Filesystem / storage layer
   ↓
systemd / service layer
   ↓
Network layer
   ↓
SSH / access layer
   ↓
Monitoring / logging layer
   ↓
Application layer
   ↓
Dependency layer
```

---

## Incident Reasoning Pattern

### Case 1: Only the website is down

```text
Website: down
SSH: working
CPU: normal
Memory: normal
Service: stopped
```

Likely failing layer:

```text
Service / application layer
```

---

### Case 2: Website, SSH, metrics, and logs are all unavailable

```text
Website: down
SSH: timeout
Monitoring: no data
Logs: not arriving
Cloud VM: running
```

Likely failing layers:

```text
Boot layer
Kernel layer
Filesystem/storage layer
systemd layer
Network layer
Resource exhaustion layer
```

This indicates a deeper system-level problem.

---

### Case 3: Application cannot reach the database.

```text
Website: down
SSH: working
CPU: normal
Memory: normal
nginx: running
App logs: database connection timeout
```

Likely failing layer:

```text
Application dependency / database / network path
```

Possible causes:

- Database server is down
- Database port is blocked
- DNS resolution failure
- Wrong database hostname
- Firewall/security group issue
- Routing problem
- Database overloaded
- Connection pool exhausted
- Invalid credentials

---

## Beginner Mistake Corrected

Common beginner thinking:

```text
SSH failed → Network problem
```

Better engineer thinking:

```text
SSH failed could mean:
- VM issue
- Boot issue
- Kernel panic
- Filesystem failure
- Network failure
- SSH service failure
- Firewall issue
- Resource exhaustion
```

The better question is

```text
What else failed at the same time?
```

---

## Key Lessons Learned

- A computer is hardware that needs software instructions.
- The operating system manages hardware safely.
- The kernel is the core of the operating system.
- Applications request kernel services through system calls.
- Linux is the kernel, not the entire operating system.
- A Linux-based OS includes a kernel, tools, libraries, services, a shell, and a package manager.
- Cloud VM running status does not guarantee Linux health.
- Troubleshooting should begin by identifying the failing layer.
- One failed component may indicate a local issue.
- Many failed components together often indicate a lower-layer failure.
- Evidence should guide root cause analysis.

---

## Memory Hooks

```text
A computer is hardware waiting for instructions.
An operating system turns chaos into controlled work.
Programs ask. The kernel decides.
VM running does not mean Linux healthy.
Symptoms tell you what is broken.
Layers help you discover where it is broken.
Evidence proves why it is broken.
```

---

## My Mastery Check

I should be able to answer these questions:

1. What are the basic functions of a computer?
2. Why does an operating system exist?
3. What is the difference between Linux and a Linux-based operating system?
4. What does the kernel manage?
5. Why do applications use system calls?
6. Why does “VM running” not always mean “Linux healthy”?
7. Why do senior engineers troubleshoot in layers?
8. If SSH, monitoring, and logs all fail together, why should I suspect a lower layer?
9. If SSH works but nginx is stopped, which layer is likely failing?
10. If the app logs show a database timeout, which layer should I investigate?

---

## Chapter Status

Status: Completed

Mastery demonstrated:

- Computer basics
- OS purpose
- Kernel role
- System calls
- VM health vs Linux health
- Layered incident thinking
- Basic SRE troubleshooting mindset

---

## Final Reflection

This chapter taught me that Linux mastery is not about memorizing commands.

Linux mastery begins with understanding layers.

A strong engineer does not immediately ask the following:

```text
Which command should I run?
```

A strong engineer first asks the following:

```text
Which layer is failing?
What evidence proves it?
What changed?
What depends on this layer?
```

This is the foundation of real Linux troubleshooting, DevOps engineering, and SRE thinking.
