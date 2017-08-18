# Learn command line

Please follow and complete the free online [Command Line Crash Course
tutorial](https://web.archive.org/web/20160708171659/http://cli.learncodethehardway.org/book/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. Each "chapter" focuses on a command. Type the commands you see in the _Do This_ section, and read the _You Learned This_ section. Move on to the next chapter. You should be able to go through these in a couple of hours.

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

* show current working directory path: $ pwd (print working directory)
* changing the working directory: $ cd directory name
* moving up one directory: $ cd ..
* creating a directory: $ mkdir directory name (make directory)
* deleting a directory: $ rm -r directory name (remove -recursive)
* creating a file using `touch` command: $ touch filename
* deleting a file: $ rm filename
* renaming a file: mv old filename new filename
* listing hidden files: $ ls -a
* listing all contents of a directory in long format: $ ls -l
* copying a file from one directory to another: $ cp directory/filename /new directory
* copying all files in the working directory to another: $ cp * directory
* moving a file from on directory to another: $ mv filename directory
* redirecting the standard output to a file: $ echo "stdin" > filename
* outputting the contents of a file to the terminal: $ cat filename
* overwriting the contents of a file to another file: $ cat original filename > new filename
* copying the contents of a file and append to another file: $ cat orginal filename >> new filename
* outputting the number of lines, words, and characters in a file: $ cat filename | wc
* sorting contents of a file: $ sort filename
* filtering out adjacent, duplicate lines in a file: $ uniq filename
* searching files for lines that match a pattern and returns the results: $ grep string filename
* searching all files in a directory and outputs filenames and lines containing matched results: $ grep -R string directory
* searching all files in a directory and outputs only filenames with matched results: $ grep -Rl string directory
* searching for a text pattern, modifies it, and outputs it: $ sed 's/search string/replacement string/g' directory
* creating and editing a file in the nano text editor: $ nano filename
* clearing the terminal window: $ clear
* opening ~/.bash_profile in nano: $ nano ~/.bash_profile
* activating the changes in ~/.bash_profile for the current session: $ source ~/.bash_profile
* creating keyboard shortcuts, or aliases, for commonly used commands: $ alias
* outputting a history of commands that were entered in the current session: $ history
* returning a list of the environment variables for the current user: $ env
* opening manual (or man) pages for any commands: $ man command

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

* ls: lists all of the files in the directory
* ls -a: lists all contents of a directory, including hidden files and directories
* ls -l: lists all contents in long format
* ls -lh: lists files with human readable format
* ls -lah: lists all contents of a directory with human readable format
* ls -t: orders files and directories by the time they were last modified
* ls -Glp: lists all contents in long format, without printing group names, and append / indicator to directories

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

* ls -a:	Displays all files.
* ls -l:	Displays the long format listing.
* ls -R:	Displays subdirectories as well.
* ls -x:	Displays files as rows across the screen.
* ls -1:	Displays each entry on a line.

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

xargs is a command on Unix and most Unix-like operating systems used to build and execute command lines from standard input. grep is an example of a xargs for searching plain-text data sets for lines that match a regular expression.

 

