# File System
list files and directories  

	ls

change directory  

	cd <path>

create a new directory

	mkdir <name>

create a new path and every directory along the path

	mkdir -p <path>

remove data

	rm <name>

Copy folders with content

	cp -avr /home/vivek/letters /usb/backup
	
Copy file type from folder and subfolder

	find dir/ -name "*.fast5" -exec mv {} Out_dir \;

Copy files with a filetype into a certain amount of subfolders:

	n=0; for f in *.fast5; do d="subdir$((n++ / 20))"; mkdir -p "$d"; mv -- "$f" "$d/$f"; done

Creating data files

	touch
	
List all files with extension

	$ ls *.fastq
	$ ls *977.fastq

Echo writes arguments
	
	$ echo *.fastq

Copy a file from system to system

	scp <source> <destination>

To copy a file from B to A while logged into B:

	scp /path/to/file username@a:/path/to/destination

To copy a file from B to A while logged into A:

	scp username@b:/path/to/file /path/to/destination

# Running commands

Run a programm in the background

	<command>&

List the ongoing processes in the background

	jobs

Bring a process in to the foreground

	fg

Kill a process in the foreground

	press control-c

Inorder to Maintain a long-Running Job

	nohub <command>
	
Repeat command with history

	$ history
	ctrl + c --> cancel comman you are writing
	ctrl + r --> reverse searach trough command history
	ctrl + l / clear --> clears screen

# File examination

examine files
	
	$ cat SRR098026.fastq
	$ less SRR097977.fastq

Some navigation commands in less

	key 		action
	Space 		to go forward
	b 			to go backward
	g 			to go to the beginning
	G 			to go to the end
	q 			to quit

Look at fastq files example (look at firs four lines)

	$ head -n 4 SRR098026.fastq

Look at file permission

	$ ls -l

 Change file permission
 
	$ chmod -w SRR098026-backup.fastq

search within files without even opening them, using grep

	$ grep NNNNNNNNNN SRR098026.fastq

aking what would ordinarily be printed to the terminal screen and redirecting it to another location

	$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq > bad_reads.txt

doesn’t require us to create these intermediate files - the pipe command (|).

	$ grep -B1 -A2 NNNNNNNNNN SRR098026.fastq | less

We can check the number of lines in our new file using a command called wc

	$ wc bad_reads.txt

# Use of foor loops
When the shell sees the keyword for, it knows to repeat a command (or group of commands) once for each item in a list

	$ foo=abc
	$ echo foo is $foo
	foo is abc
	$ echo foo is ${foo}EFG      # now it works!
	foo is abcEFG

for loop to show us the first two lines of the fastq files

	$ for filename in *.fastq
	> do
	> head -n 2 ${filename}
	> done

Basename is a function in UNIX that is helpful for removing a uniform part of a name from a list of files

	$ basename SRR097977.fastq .fastq

# Create scripts
We’ll call it bad-reads-script.sh. The sh isn’t required, but using that extension tells us that it’s a shell script.

	$ nano bad-reads-script.sh

We had to type bash because we needed to tell the computer what program to use to run this script. Instead, we can turn this script into its own program. We need to tell it that it’s a program by making it executable.

	$ chmod +x bad-reads-script.sh

 We’ll need to put ./ at the beginning so the computer knows to look here in this directory for the program
 
 	$ ./bad-reads-script.sh
 
 There are two programs that will download data from a remote server to your local (or remote) machine: wget and curl
 
 	$ wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt

# Pipeline commands
Print files to the standard output

	cat

piping to another programm

	¦

Execute command if the previous has failed

	¦¦

Execute command if the previous has completed

	&&


# Git
In oder to initialize a project directory (Firs change to the directory)

	git init

clone from Github

	git clon git:<weblink>

gives status about the repository tracked by git

	git status

# Get bioinformatics data
Downloading Data

	wgetor curl

Syncronising data over network

	rsyncor secure copy

Checking data integrity 

	shasum