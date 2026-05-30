# Java File System Manager

A command-line file management system built in Java that simulates a shell interface.

## Features

- List files and directories (`ls`)
- Navigate directories (`cd`, `pwd`)
- Create files and directories (`touch`, `mkdir`)
- Delete files and directories with recursive support (`rm`)
- Rename files and directories (`rename`)
- Search files by pattern (`find`)
- View detailed file info (`info`)

## How to Run

**Compile:**

```bash
javac FileSystemManager.java
```

**Run:**

```bash
java FileSystemManager
```

## Commands

| Command | Description |
|---|---|
| `help` | Show available commands |
| `ls` | List files in current directory |
| `cd <dir>` | Change directory |
| `pwd` | Print current path |
| `mkdir <name>` | Create directory |
| `touch <name>` | Create file |
| `rm <name>` | Delete file or directory |
| `rename <old> <new>` | Rename file or directory |
| `find <pattern>` | Search files by name |
| `info <name>` | Show file details |
| `exit` | Exit the program |

## Technologies

- Java SE (java.io, java.util, java.text)
