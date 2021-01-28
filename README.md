# run-with-lockfile

A simple utility to lck a file and then execute a program, optionally
with a timeout.

## Build

Simply run `make` and you should be good to go.

## Usage

run-with-lockfile [-ne] [-t timeout] FILE COMMAND

Open (perhaps create) and fcntl-lock FILE, then run COMMAND. If option -n
is given, fail immediately if the lock is held by another process;
otherwise, wait for the lock. When COMMAND is run, the variable LOCKFILE
will be set to FILE in its environment. If -e is given, execute the command
directly; otherwise COMMAND is run by passing it to /bin/sh with the -c
parameter.  The full path of the command should be given when -e is used.

Exit value is that returned from COMMAND; or, if -n is given and the lock
could not be obtained, 100; or, if another error occurs, 101.

If a timeout value is given with -t, the command will be killed if it runs
for longer than that number of seconds, and the exit value will be 102.
Note that, for the timeout to be effective, -e should also be used.
