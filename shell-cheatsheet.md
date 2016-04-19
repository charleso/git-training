Cheatsheet - Shell
==================

There are a number of shell commands throughout this guide,
for navigating around folders and creating/updating files.
It's perfectly acceptable to use your normal file browser
and text editor to do the same thing.

For reference the following gives a very quick explanation
of what each shell command does.


## `cd foo`

`cd` stands for "change directory".

By default your terminal will have a "current working directory",
which then determins what files you can see/edit.
This is much like having a single file browser window open,
when you double-click on a folder it will "change directory".
This command is doing the same thing.


## `ls -F foo`

List the files in the `foo` directory.

The `-F` adds a `/` to the end of directories to distinguish
them from normal files.


## `cat foo`

Displays the contants of the file `foo` on the terminal.


## `echo "abc" > xyz.txt`

Put the string "abc" into the file `xyz.txt`.
This will create the file if it doesn't already exist,
and will overwrite any content that is already there.

NOTE: This is _one_ `>` character


## `echo "abc" >> xyz.txt`

_Append_ the string "abc" on a new line in the file `xyz.txt`.
This will create the file if it doesn't already exist.

NOTE: This is _two_ `>` characters
