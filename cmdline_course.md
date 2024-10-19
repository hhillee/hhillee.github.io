---
layout: default
---


## Introduction

The course, _Command-Line Tools for Linguists_ is an introduction course to command line environment. Contents of this course starts from the basic usage and navigation of command line and builds upon previously learned skills by introducing more complex things each week.

Since the course is for linguists, the focus of the exercises and commands learned are in things that are useful for linguists specifically. This means that during the course, things such as creating frequency lists and trigrams from text files are learned.

The final project of the course is to create a website using command line and GitHub.

## Week 1 Introduction to Command Line Environments

#### Content:

The first week was all about the basics and an introduction to what exactly is a command line environment and how it works.

#### What I learned:

During the first week I learned the basics of a command-line environment.  I learned what a terminal is and how to navigate, create, move and delete files and directories. I learned to find out which directory I'm currently in, how to change directory. I also learned how to get txt files from the internet.

The following code would download the Gutenberg book of the link.

```
$ wget https://www.gutenberg.org/files/215/215-0.txt
```


## Week 2 Navigating a UNIX System

#### Content:

The second week we learned more about the UNIX system. Contents of this week were e.g. the permission classes, compressed files and remote servers.

#### What I learned:

I learned what different permission classes are and how they work. I also learned how to change them. I also learned how to connect to a remote server.

```
$ chmod 755 [FILENAME]
```

This code changes read, write and execute permissions to a file in the following way:

|         | user | group | other |
|---------|------|-------|-------|
| read    | x    | x     | x     |
| write   | x    | 0     | 0     |
| execute | x    | x     | x     |

User has all read, write and execute permissions, group and other have read and execute permissions.


## Week 3 Basic Corpus Processing

#### Content:

This week was mainly about text processing tools and structured text files. This week's material introduced useful commands for text processing such as **iconv**, **tr** and **wc**. It also included regular expressions and the command **grep** and **egrep.

#### What I learned:

I learned how to convert a text file to uft-8 encoding and how to sort a text file's lines into alphabetical order, remove duplicate lines and count the number of lines, words and characters in a text file. I also learned to search for patterns in a text file with regular expressions. I also learned to how to use the command egrep.

The following code counts how many words of a txt file starts with a lowercase "a" or uppercase "A". 

```
$ egrep -i  "^a" [FILENAME] | wc -w
```

The **-i** in the code tells _egrep_ to ignore the case, so it will count both lower and uppercase. Egrep it then piped to **wc** which stands for count and **-w** for word. The terminal will print out the word count.

## Week 4 Advanced Corpus Processing

#### Content:

This week's theme was advanced corpus processing techniques. On top of using the week's three commands, the command **sed** was introduced that was used with regular expressions. **Sed** was used for finding certain patterns and changing them.

#### What I learned:

The following code creates a sentence per line formatted txt file:

```
cat [FILENAME] | dos2unix | sed 's/^$/#/' | tr '\n' ' ' | sed -E 's/([.?!]) ([A-Z])/\1# \2/g' | sed -E 's/([IVX][.])#/\1/g' | tr '#' '\n' | sed 's/^ *//' | sed 's/ *$//' | grep -v "^$" > [FILENAME]
```

##### Explanation of the commands:
- ```dos2unix``` converts from windows line format (^M\$) to mac (^\$)
- ```sed 's/^$/#/'```  substitutes empty lines to a hash sign
- ```tr '\n' ' '``` changes line brackets (\n) to a space -> file will turn into a long row of text
- ```sed -E 's/([.?!]) ([A-Z])/\1# \2/g'``` change sentence end characters to a hash sign
	- ```-E``` use extended regular expressions
	- ```([.?!]) ([A-Z])``` creating sets 1 (sentence end characters) and 2 (capital letters)
	- ```\1# \2``` substitute to set 1 followed by a has sign and set two
	- ```g``` use for every instance
- ```sed -E 's/([IVX][.])#/\1/g'``` if a set includes roman numbers followed by a period, delete period
- ```tr '#' '\n'``` translate a hash sig to an unix line -> one sentence per line
- ```sed 's/^ *//'``` get rid of spaces in front of lines
- ```sed 's/ *$//'``` get rid of spaces at the end of a line
- ```grep -v "^$"``` grab every line that does not contain an empty line (to get rid of extra space between lines)
- ```> [FILENAME]``` redirects standard output to a new file

## Week 5 Scripting and Configuration Files

#### Content:

This week's theme was configuration files and scripts. Content of this week included; what are scripts and how to write them, what are environment variables and how to use them as well as modifying configuration files to create a nice looking working environment.

#### What I learned:

This is exercise 6 from the week's quizz where I had to build a script that takes the attached adjectives.txt file as an argument and prints its comparative form. 

```
#!/bin/bash

  
# Check if a file is provided

if [ "$#" -ne 1 ]

then

  echo "ERROR: A file needed"

  echo "$0 input_file_text"

  exit 1

fi

  
# Read every line of the file and print in terminal

while read -r line;

 do comparative="${line}er"

  echo "$comparative"

done < $1
```

- ```#!/bin/bash``` tells this file is a script and should be interpret as one
- ```if``` starts an if-loop
- ```[ "$#" -ne 1 ]``` checks if a file is provided
- if not prints an appropriate message to the terminal
- ```fi``` end of the if-loop
- ```while read -r line;``` read every line of the file
- ```do comparative="${line}er"``` and create a comparative form
- ```echo "$comparative"``` then print 
- ```done < $1``` end of while-loop and tells what the standard input is

## Week 6 Installing and Running Programs

#### Content:

Learning to install programmes: softwares and python packages. Learning to use makefiles. Learning commands such as ```sudo``` and ```brew```.

#### What I learned:

Creating makefiles

```
results/%.freq.txt: data/%.no_md.txt 

        src/freqlist.sh $< > $@
```

A make rule where the ```src/freqlist.sh``` script is run on all of the  ```%.no_md.txt ``` files from the data-directory and place in the results-directory with a new name ```%.freq.txt```. 

## Week 7 Version Control

#### Content:

Theme of week 7 is version control. What it is and why it is useful. Learning how to use. Introduction to GitHub and setting it up.

#### What I learned:

I created my GitHub page and worked on the cmdline-course project for the week 7 where I for example edited makefile. I learned to **add**, **commit** and **push** changes to GitHub.

Here's a lovely picture of my _activity_ tab of the project.

! [activity log] (https://github.com/hhillee/hhillee.github.io/blob/cmdline-course/assets/img/activity_tab.png)

### Week 8  Final project

Week 8 is about working on the final project which this webpage essentially is. I learned how to fork in GitHub and create my own website using a template and all this cool stuff. Overall this has been a very useful course.


