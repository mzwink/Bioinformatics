#### Shell Scripting


Chapter 12 BDS

---

File and directory test expressions

	-d dir		dir is a directory
	-f file		file is a file
	-e file 	file exists
	-h link		link is a link
	-r file		file is readable
	-w file		file is writable
	-x file 	file is executable
	
Combine these to check if a file is in a directory and if you can write to it

	if test -f some_file.txt
	then
		[...]
	fi
	
Bash has a simple syntactive alternative:

	if [ -f some_file.txt ] #must have space around brackets
	then
		[...]
	fi
	
We can chain expressions with -a as logical AND -o as logical OR, ! as negation

	#!/bin/bash
	set -e
	set -u
	set -o pipefail
	
	if [ "$#" -ne 1 -o ! -r "$1" ]
	then 
		echo "usage: script.sh file_in.txt"
		exit 1
	fi
	
					