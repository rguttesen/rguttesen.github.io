---
layout: default
---

## Introduction

The Command Line is essentially a text-based user-interface, allowing the user to communicate with the computer textually rather than visually, which tends to be te norm these days. Using the Command Line does open up many new possibilites, however, and many of its functions are priceless when conducting, say, linguistic inquiry; in certain cases the functions are unusable outside the Command Line environment.

## Week 1: The Command-Line Environment

During the first week we were introduced to the command line environment and to some basic commands, such as `cat`, `mv` and `cp`. We also learned about directories: how to navigate directories with `cd`, make directories with `mkdir` and remove them with `rmdir`. During the quiz of the week, we were also tought the `echo` command along with output redirection using `>`.

## Week 2: UNIX

During this week we learned about access permissions: a file can have three levels of permissions - read, write, execute - for three different entities - user, group, other. The access permissions of a file can be easily viewed with `ls -l`, and the permission can be represented either symbolically (e.g. `-rw-rw-r--`) or numerically (e.g. `664`). Changing the permissions of a file can be done with the `chmod` command which can also be used symbolically or numerically; for example, giving read permission to everyone, write permission to the group, and execute permission to the user can be accomplished with both of these commands:
```
$ chmod 764 file.txt
$ chmod u+rwx,g+rw,o+w file.txt
```
Another theme of this week was processes. Using `top` you can see all processes that are currently running, along with their process ID, or PID; giving a PID after the command `kill -q` will termine the process of the given PID. Somewhat in the same vein, a command resulting in a lengthy process can be moved to the background using `&`, allowing the user to keep using the command prompt while the command is runnging. For example:
```
$ rm -R home &
```

## Week 3: Basic Corpus Processing

This week's material was definitely the most applicative to linguistic inquiry so far. We learned about the most common text encoding systems, such as ASCII and UTF-8, and also about converting files between different encodings with the `iconv` command; finding out the encoding type of a text file can be achieved with the `file` command, and line, word and byte counts can be checked with the command `wc`. The two most-used commands this week were unquestionably `sort` and `uniq`; the former sorts all lines in a text file in alphabetical order, and the latter removes duplicate lines from a text file. Common options used with these commands are `sort -f` and `uniq -i`, which both ignore case, `sort -n`, which sorts the lines numerically, `sort -r`, which sorts the lines in a reverse order, and `uniq -c`, which counts the duplicate lines instead of removing them.

## Week 4: Advanced Corpus Processing

This week we took our text-processing skills to a new level. We learned about "piping" commands using `|`, which allows you to chain multiple commands together in the command line; doing this with the commands learned last week, we are able to create, for instance, a list of word frequencies in a text file. But before attempting this, we still need to understand the `sed` command, which can be used to print, delete and replace text in a file using regular expressions. Let's consider the command down below:
```
$ sed -nE 's///g'
```
This command has the option `-nE`, which tells the command to print only matching lines and to use extended regular expression. The part `'s///g'` is used to replace the text that's between the first and second slash with the text that's between the second and third slah; of course, at this point the command does nothing since both spaces are empty, and we also need a file to be opened as input. Consider the full command below:
```
$ sed -nE 's/a/A/g' textfile1.txt > textfile2.txt
```
This command replaces all instances of lowercase a in textfile1 with a capital A and then saves that in a new textfile called textfile2. Now, Let's look at all the individual steps we have to do in order to create a word-frequency list of a textfile:
1. Remove punctuation so all words are only separated by spaces
2. Replace all spaces with new lines so all words have their own lines
3. Sort the file so that all words (i.e. lines) appear alphabetically
4. Count how many times lines appear in the file
5. Sort the file so that the highest number is at the top

Now we can finally have a look at the full command which turns creates a word-frequency list (textfile2.txt) of the words in textfile1.txt; notice how all steps in the list above are separated by the pipe in the command, and also that the `sed` command does not have the option `-n`, since we want to chain the entire input file between commands, not just the matching lines.
```
$ sed -E 's/(\. |, |\? |! |: |; )/ /g' testfile1.txt | sed -E 's/ /\n/g' | sort -f | uniq -ic | sort -nr  > testfile2.txt
```

## Week 5

## Week 6

## Week 7