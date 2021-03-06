Lecture Notes - CSCE 215 UNIX/Linux Fundamentals 8:30 - 9:20 a.m.
=================================================================

## 25 Oct. 2017
* On paper

## 30 Oct. 2017
* To copy from remote machine: `scp -P222 hdamron@L-1D39-18.cse.sc.edu:[remote file] [local destination]`
* `>` rewrites destination; `>>` appends to destination file (creates if exists)
* Unix System Structure
 * user -> shell and utilities -> kernel -> hardware
* Shell
 * User interface to operating system
 * REPL
 * Examples
  * sh - Bourne shell / POSIX shell
  * csh - C shell
  * tcsh - Enhanced C shell
  * ksh - Korn shell
  * bash - Borne Again Shell (Free ksh clone)
 * Waits for user input and parses input
 * (CSCE 510 is shell creation)
* Shell script
 * File containing shell commands which is labeled executable
* Shell commands
 * Simple command: sequence of non-blank arguments separated by blanks or tabs
  * Arg 0 is name of command, others are parameters to that command
* Linux heirarchy
 * / - root
 * /bin/ - executables
 * /acct/ - user accounts (on lab machines)
* Prompt symbol (in bash)
 * $ regular user
 * # super user
* Types of Arguments
 * Options/Flags
  * convention -X or --longname (where X is single char shortname)
* Man page
 * man [command]
* Users and Groups
 * Each user belongs to main group and can have other groups
 * Each file has separate r,w,x permissions for specific user,group,everyone
* Filename
 * Relative path: path relative to current directory
 * Absolute path: path from root (starts with /)
* Working directory: where process is currently located
* Mounting file systems:
 * In Linux lab, home directories are mounted on /acct/ (rather than usual /home/)
* `cat` outputs file contents to stdin (can be rerouted to file)
 * `-v` displays hidden characters
* Common utilities
 * `pwd` print working directory
 * `ed`, `vi`, `emacs`, `nano` - text editors
 * `wc` counts patterns
* Directory permissions
 * read: can access
 * write: can create inside
 * execute: can cd into
* `chmod` number scheme
 * For r-w-x, binary number (i.e. read, !write, execute = 101 = 5)
* Tree walking
 * possibility: `ls -l -R /`
* `find` command makes tree walking easier
 * `find [location] [patterns]`
  * `-name "{pattern}"` searches by file name
  * others are:
   * `perm [num]` by permissions
  * actions come after patterns:
   * `-print` default
   * `-exec [command] [args] \;` (to use filename from find use {})


## 1 Nov, 2017
* Manipulating file attributes
 * `chmod` - change permissions
 * `chown` - change file owner
 * `chgrp` - change group
 * Note: only super user and owner can change attributes of file
 * `umask` is default value of creation
 * Examples
  * 755 `-rwxr-xr-x`
  * 644 `-rw-r--r--`
* Std(in/out/err)
 * stdin 0
 * stdout 1
 * stderr 2
 * reroute only stderr: `2>`
 * `/dev/null` is infinite trash can
* Links
 * directory entries are not physical files but links to the desired files
* Processes
 * All processes are unique
 * `ps -ef` lists all processes including root processes
  * `ps` without `-ef` shows only user processes
 * `grep` searches for lines containing regex pattern
 * `who` shows users on the machine
 * program: collection of bytes stored in executable file which can be run
 * image: computer execution environment of program
 * `kill` kills jobs (`-9` arg forces now without waiting)
* Background jobs
 * Appending `&` to end of line in terminal pushes command to the background (meaning shell does not wait for output)
* Program arguments
 * when process starts, it is sent a list of strings (argv and argc = argument vector and count, respectively)
* Shebang: `#!/bin/sh` specifies that script should be run in  Bourne shell
 * Other possibilities include `#!/bin/bash`, `#!/bin/perl`, `#!/bin/python`, etc.
* Cmd args in sh script
 * `$0` gives program name itself
 * `$1`...`$n` gives subsequent arguments if they exist (calling empty variable gives empty string)
* Return codes
 * 0 is success, everything else is some form of error
* Environment of process
 * Variables and more available to the process
 * `echo $PATH` shows all path variables (variables which can be used to execute from anywhere)
 * `export PATH=.:$PATH` adds current directory to front of existing path (extremely bad idea because items in current directory override system utilities)
* `which [command]` tells where the command is located

## 6 Nov. 2017
* Environment variables
 * var=value #sh, bash
 * set var = value #ksh
* Important variables
 * `HOME` = user home directory
 * `PATH` = : delimited directories for command lookup
 * `USER` = username
 * `MAIL` = absolute path of mailbox
 * `SHELL` = absolute path of login name
 * `TERM` = terminal type
 * `PS1` = terminal prompt
* Process subsystem utils
 * `ps` = monitor status of processes
 * `kill` = send signal to pid
 * `wait` = parent process waits for one of its children
 * `nohup` = makes command immune to hangup and terminate signals
 * `sleep` = sleep time in seconds
 * `nice` = run processes in low priority
* Pipes
 * redirects output of one command to input of another command
 * makes filters
* `cat file | command` = `command < file`
* Filter examples
 * `sort` = sorts lines from a file by user specified pattern
 * `grep` = string matching filter
 * `awk` = programmable filter
 * `cat` = simplest filter: outputs file to stdout
 * `head` = first n lines of file
 * `tail` = last n lines of file
 * `cut` = prints selected parts of lines
  * file delimiters: Tab/Pipe/Colon/Comma-separated
  * `-d` delimiter type
  * `-f` field number (i.e. 1) or numbers (i.e. 1-3)
  * `-c` character number or numbers
  * unfortunately there is no way to count backwards from last char/field
 * `uniq` = remove or report _adjacent_ unique lines
  * good idea to sort first because unique lines must be adjacent
 * `wc` = counts results
   * `-l` counts lines
   * `-m` counts chars
   * `-w` counts words
 * `tr` = translate or delete characters
  * `tr [from_pattern] [to_pattern]` converts lines of first pattern to second pattern
  * i.e. `tr A-Z a-z` converts uppercase letters to lowercase letters
  * just prints to stdout, does not change file
 * `sed` = pattern matching with action
  * possibly delete every other line: `sed n'd'`
 * `file` = tries to tell type of file

## 15 Nov. 2017
 * `gitk` = git repository browser
 * Debuggers
  * `-g` parameter with `cc`, `gcc`, and `g++`
  * `gdb [programfile] [<corefile>|<pid>]]`
 * `gdb` commands
  * Shown too quickly
 * `make` - Compilation helper using `Makefile`
  * Example Makefile
   * Shown too quickly
 * `tar` Options
  * `-c` compress
  * `-f filename` specify tar format file
  * `-v` verbose
  * `-x` extract
  * `-t` table of contents
