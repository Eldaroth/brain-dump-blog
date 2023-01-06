---
title: "Background & Foreground Processes"
subtitle: "Linux Foundations"
date: 2023-01-06T19:12:36+01:00
tags: ['linux', 'cli']
draft: true
---
Linux organizes different programs being run or waiting for CPU resources in processes. If one of these programs becomes slow or even stops responding, Linux offers various tools for examining processes and terminating those which are misbehaving.

<!--more-->

The kernel monitors and maintains information about each process running on a Linux machine. For example, when the system starts up, the kernel initiates some processes itself and launches a program called `init.init`. This program then runs a series of so called **init scripts** (shell scripts located in `/etc`) which start all the system services. A lot of these services are **daemon** programs - they run and wait in the background for any input from the system or user (*daemons* usually don't have any user interface though). Processes launched by other programs are called **child process**, while the program or process launching it is known as **parent process**.

For monitoring, the system assigns each process a number called "process ID (PID)". We can view running processes with the command `$ ps`. The command by itself does not show very much, only the processes associated with the current terminal session:

![ps_screen.png](/img/ps_screen.png)

By adding the option `x` to the command, the terminal gives back a bigger picture with all of the processes currently running:

![ps_x_screen.png](/img/ps_x_screen.png)

The column **STAT** stands for "state" and shows the current status of the process, such as *R = Running*, *S = Sleeping*, *T = Terminated (Stopped)* etc. More information about the various states can be found on the man page for `ps`.

There are other combination of options which can be used to even display more information - one other popular set of options is `aux`. Try it out and see what comes back.

## Dynamic tools
Apart from the `ps` command, there are other programs which show a more dynamic view of what the machine currently is doing.

The `top` program is installed on most Linux systems and displays a continuously updating list of system processes in order of their activity. Ubuntu for example also knows `htop` which is graphically more pleasing and offers more options to interact with the information provided than `top` does.

Personally, I use [`btop`](https://github.com/aristocratos/btop), a resource monitor written in C++ which also shows stats for CPU, memory, disk and network usage besides listing all running processes. Somewhat akin to the Windows Task Manager - only in CLI form.

## Putting commands in the background

When we enter a command in the terminal, it usually is run in the foreground and we have to wait until the job is completed. As long as this only takes a couple of seconds, its usually no problem. However, if the job we are trying to execute takes a long time to complete, this can be kind of a nuisance.

Luckily, Linux provides the option to run commands we want to execute in the background.

**Foreground:**
* run directly from the shell
* when a job is running, other jobs need to wait (in the same terminal window)
* jobs can be run in the background

**Background:**
* will be executed at lower priority
* allows other jobs to be executed in the foreground

## Commands

Put a job in the background by suffixing `&` to the command:
`$ sleep 100 &`

* Alternatively, use **Ctrl + Z** to suspend a foreground job and **bg** to put it in the background
* Bring it back to foreground with **fg**

![bg_cmd_screen.png](/img/bg_cmd_screen.png)

***

### Sources
* Shotts, William (2019). The Linux Command Line. Fifth Internet Edition.
Link: [http://linuxcommand.org/](http://linuxcommand.org/)