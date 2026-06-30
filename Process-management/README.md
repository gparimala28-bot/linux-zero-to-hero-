# ⚙️ Linux Process Management

## 🖥️ What is Process Management?

A **process** is a running instance of a program. Linux uses process management to create, schedule, monitor, and control processes efficiently while allowing multiple programs to run simultaneously.

Process management helps administrators:

* Run multiple programs at the same time
* Allocate CPU and memory efficiently
* Monitor running processes
* Control process execution
* Manage system services (daemons)

> 💡 **Why it matters:** Every application you run in Linux becomes a process. Understanding processes is essential for system administration, troubleshooting, and performance optimization.

## 🧩 Process Resources

Every process has its own resources:

* Process ID (PID)
* Parent Process ID (PPID)
* Memory (RAM)
* CPU Time
* Process State

> Linux isolates each process so that one process does not interfere with another.

## 🆔 Process Identification

Every process is uniquely identified by:

* **PID (Process ID)** – Unique identifier
* **PPID (Parent Process ID)** – ID of the process that created it

Example:

```text
bash (PID 2000)
        │
        ▼
python hello.py (PID 2500)
```
## 🔄 Process Life Cycle

Every process goes through several states:

```text
Created
   │
   ▼
Ready
   │
   ▼
Running
   │
   ▼
Waiting
   │
   ▼
Running Again
   │
   ▼
Finished
```
Linux automatically manages transitions between these states.

## 🌳 Process Hierarchy

Processes are organized as a parent-child tree.

Example:

```text
systemd
│
├── sshd
│     └── bash
│            └── python
│
└── nginx
```

View the hierarchy using:

```bash
pstree -p # Displays processes in a tree format along with their PIDs.
```
## ⚙️ Daemon Processes

A **daemon** is a background process that runs continuously and provides system services.

Examples:

* systemd
* sshd
* nginx
* cron

Characteristics:

* Starts automatically during boot
* Runs without a terminal
* Provides continuous services

## 🖥️ Foreground vs Background Processes

### Foreground Process

Runs in the terminal and blocks it until completion.

```bash
python app.py # Starts the Python program in the foreground and occupies the terminal.
```

### Background Process

Runs while allowing the terminal to remain usable.

```bash
python app.py & # Starts the Python program in the background and keeps the terminal available.
```

## 👀 Viewing Processes

| Command  | Purpose                         |
| -------- | ------------------------------- |
| `ps`     | Show process snapshot           |
| `ps -ef` | Show all processes with details |
| `ps aux` | Detailed process information    |
| `top`    | Real-time process monitoring    |
| `htop`   | Interactive process viewer      |
| `pstree` | Display process hierarchy       |


## 🔍 Finding Processes

```bash
pgrep nginx  # Find the PID of processes named nginx
```

```bash
pgrep -l ssh # Displays the PID along with the matching process name.
```

```bash
pidof sshd # Returns the PID of the sshd executable.
```

## 🛑 Process Signals

Linux controls processes using signals.

| Signal  | Purpose                        |
| ------- | ------------------------------ |
| SIGTERM | Gracefully terminate           |
| SIGKILL | Forcefully terminate           |
| SIGSTOP | Pause process                  |
| SIGCONT | Resume process                 |
| SIGINT  | Interrupt (Ctrl+C)             |
| SIGHUP  | Reload configuration / Hang-up |

Examples:

```bash
kill PID # Sends SIGTERM to gracefully stop a process.
kill -9 PID # Forcefully terminates a process using SIGKILL.
kill -STOP PID # Temporarily pauses a running process.
kill -CONT PID #  Resumes a paused process.
```

Kill by name:

```bash
pkill nginx # Stops all processes whose names match "nginx".
killall firefox # Terminates every running Firefox process.
```

## ⚡ Process Priority

Linux schedules processes using **Niceness**.

Range:

```text
-20   Highest Priority
 0    Default
19    Lowest Priority
```
Commands:

```bash
nice -n 10 ./script.sh # Starts a new process with a lower CPU priority.
```

```bash
renice -n -5 -p PID # Changes the priority of an already running process.
```

## 🎯 Job Control

A **job** is a process started from the current shell.

Useful commands:

```bash
jobs # Lists all background and suspended jobs started from the current terminal.
fg %1 # Brings Job 1 back to the foreground.
bg %1 # Resumes Job 1 in the background.
```

Keyboard shortcuts:

```text
Ctrl + C → Stop process
Ctrl + Z → Suspend process
```

## 🚀 Long Running Processes

Keep processes running even after closing the terminal.

```bash
nohup ./backup.sh & # Runs the program even after the terminal is closed.
```

Remove a job from shell management:

```bash
disown # Removes a job from the shell's job list while allowing it to continue running.
```

## 📊 Monitoring Resource Usage

| Command  | Purpose                                              |
| -------- | -------------------------------------------------    |
| `time`   | Measures how long a command takes to execute.        |
| `lsof`   | Lists all files currently opened by processes.       |
| `vmstat` | Displays CPU, memory, swap, and process statistics   |
| `iostat` | Shows CPU usage and disk input/output statistics.    |
| `sar`    | Displays historical system performance reports.      |

## 🔄 Linux Process Management Workflow

The diagram below summarizes the typical lifecycle of a process—from a program stored on disk to its execution, monitoring, management, and termination.

```text
Program
   │
   ▼
User Executes Program
   │
   ▼
Linux Creates Process
   │
   ▼
PID Assigned
   │
   ▼
CPU & Memory Allocated
   │
   ▼
Running
   │
   ▼
Monitor
(ps, top, htop)
   │
   ▼
Control
(kill, nice, jobs)
   │
   ▼
Process Terminates
   │
   ▼
Linux Frees Resources
```

> 💡 This workflow shows the complete journey of a Linux process, from execution to termination.

## 🎯 Key Takeaways

- A **process** is a running instance of a program, and every running application in Linux is managed as a process.
- Every process has a unique **PID** and a **PPID** that identifies the process which created it.
- Linux allocates CPU time and memory independently for each process, ensuring isolation and system stability.
- Processes move through different states such as **Created, Ready, Running, Waiting, and Finished** during their lifecycle.
- Background services called **daemons** run continuously without user interaction and provide essential system functionality.
- Linux provides tools like **ps, top, htop, and pstree** to view, monitor, and troubleshoot running processes.
- Processes can be controlled using **signals**, adjusted with **nice/renice**, and managed from the shell using **jobs, fg, bg, nohup, and disown**.
- Performance monitoring tools such as **time, vmstat, iostat, lsof, and sar** help analyze CPU, memory, disk, and process activity.
- Understanding process management is a fundamental skill for Linux administration, DevOps, troubleshooting, and performance optimization.
