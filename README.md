# Java File System Manager

A Java command-line application that provides Unix-inspired commands for navigating, inspecting, and manipulating the local file system.

The project focuses on Java file handling, recursive directory traversal, command parsing, input validation, and error handling.

---

## Features

* Interactive shell-style command-line interface
* Navigate directories using `cd` and `pwd`
* List directory contents with size and modification timestamps
* Create files and directories
* Rename files and directories
* Delete individual files and empty directories
* Recursively delete non-empty directories with confirmation
* Recursively search for files and directories by name
* Inspect filesystem metadata and permissions
* Handles missing files, invalid commands, duplicate names, and failed operations

---

## How to Run

### Requirements

A Java Development Kit (JDK) is required.

Verify that Java is installed:

```bash
java -version
javac -version
```

### Setup

Clone the repository:

```bash
git clone https://github.com/joaoeliazar/java-file-system-manager.git
cd java-file-system-manager
```

Compile the project:

```bash
mkdir -p out
javac -d out src/*.java
```

Run:

```bash
java -cp out Main
```

The application will start an interactive shell:

```text
Welcome to the File System Manager!
Type 'help' to see available commands.

/current/path>
```

---

## Commands

| Command | Description |
| --- | --- |
| `help` | Display all available commands |
| `ls` | List files and directories in the current directory |
| `cd <directory>` | Change the current working directory |
| `pwd` | Print the current directory path |
| `mkdir <name>` | Create a directory |
| `touch <name>` | Create an empty file |
| `rm <name>` | Delete a file or directory |
| `rename <old> <new>` | Rename a file or directory |
| `find <pattern>` | Recursively search for matching names |
| `info <name>` | Display filesystem metadata |
| `exit` | Exit the application |

---

## Example

```text
> mkdir demo
Directory created: demo

> cd demo

> touch notes.txt
File created: notes.txt

> ls
Type | Size (bytes) | Last Modified       | Name
-------------------------------------------------
 -   |           0 | 2026-09-06 18:00:00 | notes.txt

> info notes.txt
Information for: notes.txt
----------------------------------
Type:          File
Path:          /path/to/demo/notes.txt
Size:          0 bytes
Readable:      true
Writable:      true
Executable:    false
Hidden:        false

> rename notes.txt project-notes.txt
File renamed from notes.txt to project-notes.txt

> find project
[File] project-notes.txt

> rm project-notes.txt
File deleted: project-notes.txt
```

---

## Recursive Operations

### Directory Search

The `find` command recursively traverses directories starting from the current working directory.

For a structure such as:

```text
projects/
├── README.md
├── java/
│   └── Main.java
└── archive/
    └── OldMain.java
```

Running:

```text
find Main
```

can locate entries in nested directories rather than searching only the current directory.

---

### Recursive Deletion

When `rm` targets a non-empty directory, the application asks for confirmation before deleting anything:

```text
Warning: Directory is not empty. Delete anyway? (y/n)
```

If confirmed, the directory tree is recursively traversed so that child files and directories are removed before the parent directory.

This prevents the application from attempting to delete a non-empty directory directly.

---

## File Information

The `info` command displays metadata about a selected file or directory, including:

* Entry type
* Absolute path
* Size
* Last modification time
* Read permission
* Write permission
* Execute permission
* Hidden status

For directories, it also reports the number of immediate files and subdirectories.

---

## Project Structure

```text
java-file-system-manager/
├── src/
│   ├── Main.java
│   └── FileSystemManager.java
├── .gitignore
└── README.md
```

### `Main.java`

Contains the application entry point and starts the file-system manager.

### `FileSystemManager.java`

Contains the interactive command loop, command parsing, path handling, filesystem operations, recursive search, recursive deletion, and error handling.

---

## Technologies

* Java
* `java.io.File` for filesystem interaction
* `java.util.Scanner` for interactive input
* `SimpleDateFormat` for file timestamps
* Recursive directory traversal
* Object-oriented programming
* Command-line application design

---

## Design Decisions

### Recursive traversal

Filesystem directories naturally form a tree:

```text
directory
├── file
└── directory
    ├── file
    └── directory
```

Recursive methods are used for operations that may need to visit an unknown number of nested directories.

Both searching and deleting directory trees use this approach.

---

### Confirmation before destructive operations

Deleting a non-empty directory can permanently remove multiple files.

Instead of immediately performing recursive deletion, the application requires explicit confirmation:

```text
Delete anyway? (y/n)
```

This adds a basic safeguard around destructive filesystem operations.

---

### Separate application entry point

`Main.java` only starts the application:

```java
new FileSystemManager().start();
```

The filesystem logic remains inside `FileSystemManager`, keeping application startup separate from command processing and file operations.

---

## Error Handling

The application handles common problems such as:

* File or directory does not exist
* Duplicate file or directory names
* Missing command arguments
* Invalid directories
* Failed file creation
* Failed deletion
* Failed rename operations
* Unknown commands

Errors are reported to the user without terminating the interactive shell.

---

## Known Limitations

* Uses a local filesystem only
* No copy or move commands
* Search uses substring matching rather than advanced glob or regex patterns
* No command history or tab completion
* No symbolic-link-specific handling
* File names containing spaces may not work with every command
* Recursive operations are synchronous
* No automated test suite yet

---

## Roadmap

* [ ] Add automated unit tests
* [ ] Add GitHub Actions CI
* [ ] Add `cp` and `mv` commands
* [ ] Improve search with glob or regex support
* [ ] Add confirmation options for destructive operations
* [ ] Improve handling of paths containing spaces
* [ ] Add command history
