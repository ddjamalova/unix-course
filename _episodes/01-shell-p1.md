---
title: "Unix commands - Part I"
teaching: 10
exercises: 4
date: 2025-04-23
doi: "https://doi.org/10.5281/zenodo.582600"
questions:
- "What is a command shell?"
objectives:
- "FIXME"
keypoints:
- "FIXME"
---

## What is a command shell?

On Unix, every user has a unique user name. When they log onto the system, they are placed in a home directory, which is a portion of the disk space reserved just for them. When you log onto a Unix system, your main interface to the system is  called the Unix Shell. This is the program that presents you with the dollar sign (`$`) prompt. This prompt means that the shell is ready to accept your typed commands. It is often preceded by the user name as well as the current directory.

Unix commands are strings of characters typed in at the keyboard. To  run a command, you just type it in and press the *Enter* key. We will look at several of the most common commands below.
Commands often have _parameters_, e. g. a file to work on. Theses are typed in after the command and are separated by spaces, e. g. `less pi_results.txt` opens the file `pi_results.txt` for reading.
 
In addition, Unix extends the power of commands by using special flags or *switches*. Switches are usually preceded with a dash (`-`), e. g. `ls -lh`.

> ## List of commands
> 
> | Command             | Description                                                  |
> | ------------------- | ------------------------------------------------------------ |
> | `pwd`               | print current (working) directory            |
> | `ls`                | list contents of the current directory                       |
> | &#10551; `-l`    | **l**ong (detailed) listing |
> | &#10551; `-h` | with **h**uman readable numbers |
> | `cd`                | change to another directory                                  |
> | `mkdir`             | make a new directory                                         |
> | `mv`                | move or rename a file or directory                           |
> | `cp`                | copy file                                                    |
> | &#10551; `-r`       | copy directory tree (**r**ecursively)                        |
> | `file` | determine file type |
> | `echo`              | print a line of text                                   |
> | `head`              | View the first 10 lines of a file |
> | `sort`              | Sort lines of text files |
> | `less`              | display contents of a file (press q to quit)                 |
> | `tail` | output the last part of a file |
> | &#10551; `-f` | **f**ollow appended data as the file grows |
> | `grep`              | list text lines containing a particular string of text |
> | &#10551; `-v` | output only non-matching lines |
> | `wc` | count lines, words, and bytes in a file |
> | `cat`               | concatenate (combine) two or more files                      |
> | `df`                | show disk free information                                   |
> | &#10551; `-h` | with **h**uman readable numbers |
> | `find`              | find files in a directory tree                               |
> | `man`               | display program manual for a command                         |
> | `ps -x`         | list one's own running programs / processes (e**x**tended list) |
> | `kill`              | kill process                                                 |
> | &#10551; `-9`       | kill process immediately (SIGKILL=**9**)           |
> | `rm`                | remove a file                                                |
> | &#10551; `-r`       | remove a directory tree (**r**ecursively)                    |
> | `rmdir`             | remove an empty directory                                    |
> | `chmod`             | change mode (security permissions) of file or directory      |
> | &#10551; `ugo+-rwx` | **u**ser (owner), **g**roup, **o**ther (world), add(**+**), remove(**-**), **r**ead, **w**rite, **e**xecute |
> | `./myprogram` | run the local executable file `myprogram` |
> | `sed 's/ab/cd/'` | transform text, e. g. replace all occurrences of 'ab' with 'cd' |
> | `nano` | Command line text file editor | 
> | &#10551; `Ctrl-x`       | By using the key combination `Ctrl-x` in the editor, you can exit the editor and optionally save the file.|
> | `wget` | network downloader (downloads files from the Web) |
> | `gzip` | compress a file |
> | `gunzip` | uncompress a file |
> | `*`                 | wildcard representing any combination of characters          |
> | **Places** |  |
> | `~`                 | your home directory                                          |
> | `.`                 | current directory                                            |
> | `..`                | parent directory                                             |
> | **Pipes** |  |
> | `>`                 | send output to a file                                        |
> | `>>`                | append (add) output to a file                                |
> | `\|`                 | pipe output from one command as input to another             |
>
> Download as [PDF](../data/cheatsheet.pdf) or separate [MarkDown](../data/cheatsheet.md).
> 
{: .keypoints}

## **Tutorial**

During this tutorial you will use many of the **commands above**. Your task is to **identify** 
**the correct commands and execute them**. Feel free to experiment. Take a look at the 
solution if absolutely necessary.

This tutorial is based on the [tutorial](https://gitlab.ub.uni-bielefeld.de/denbi/unix-course) that was created by the de.NBI Cloud Bielefeld administrators.
The first two sections (01 and 02) describe how to access the workshop environment for this tutorial.
Participants need a web browser and an active ELIXIR account. 

### **Part 1**

#### **01 - Accessing SimpleVM**

When accessing a Unix system running as a virtual machine in the cloud one would normally log into it via SSH and would be getting presented with a terminal.
For the sake of this tutorial the access route to the terminal is via web browser.
Every participant has access to a prepared virtual machine running a web-based development environment called Theia IDE.

> ## Generate a new ssh key
> You can generate a new SSH key on your local machine. After you generate the key, you can add the public key to your account on GitHub.com to enable authentication for Git operations over SSH.
> ```bash
> ssh-keygen
> ```
> {: .source}
> 
> This creates a new SSH key, using the provided email as a label.
> When you are prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location.
> 
> Please note that if you created SSH keys previously, ssh-keygen may ask you to rewrite another key, in which case we recommend creating a custom-named SSH key.
> To do so, type the default file location and replace id_ALGORITHM with your custom key name.
> ```
> Enter a file in which to save the key (/home/YOU/.ssh/id_ALGORITHM):[Press enter]
> ```
> {: .output}
> At the prompt, type a secure passphrase.
> ```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
> ```
> {: .output}
> 
{: .callout}

#### **Accessing Theia IDE**

This workshop is powered by [SimpleVM](https://cloud.denbi.de/about/project-types/simplevm/).
Every participant should have received a mail containing the actual link to their VM.
If you did not receive a mail containing a link to a VM, please contact your tutor.

After successful login the Theia IDE screen appears. The screen is usually divided into 3 sections:
Editor pane in the center, file browser on the left, terminal at the bottom.
This tutorial will primarily focus on the use of the terminal.

> ## Access your private VM
> Access to your own private virtual machine works different from what is used here. You would usually run an SSH client to connect to the machine using a key file and would then be presented with a single terminal command prompt, e.g.:
> 
> ```bash
> ssh -i ~/.ssh/mykeyfile ubuntu@myprivatevm.example.com
> ```
> {: .source}
{: .callout}


#### **02 - Opening a terminal window**

If not yet open go to -> _Terminal_ -> _new Terminal_ to open a new terminal.

![Opening a terminal window](../assets/img/Terminal.png)

It is possible to have more than one terminal open at the same time.


#### **03 - Creating a directory to work in**

Before we actually start clone this github repository so we have all files in place we need for this small exercise.

```bash
cd ~
git clone https://github.com/deNBI/unix-course.git
```

This will create the directory `unix-course` within your user's home directory.
We can now move on with the exercise.

> ## Tasks
> 1. Open the manual page of the command `pwd` by entering `man pwd`.
> 2. Find out your current (working) directory. *(1 command)*
> 3. If your current directory is not your home directory, please move to it. *(1 command)*
> 4. Now create a directory called `pi_calculation` and enter the new directory. *(2 commands)*
> 5. Confirm that your current directory has changed. *(1 command)*
>
> > ## Solution
> > ```bash
> > pwd
> > cd ~
> > mkdir pi_calculation
> > cd pi_calculation
> > pwd
> > ```
> {: .solution}
> 
{: .challenge}


#### **04 - Running a simple program**

A simple program that (slowly) approximates the number pi is available as a file at `~/unix-course/calculate_pi`.

> ## Tasks
> 1. Please copy this program into your current directory. *(1 command)*
> 2. Inspect the file you just copied to get information about its file type. *(1 command)*
> 3. Please make the file executable (for you as the owner only). *(1 command)*
> 4. Now run the executable and watch how the pi approximation gets better over time. *(1 command)*
> 5. Stop the running program by pressing the key combination `Ctrl+c`.
>
> > ## Solution
> > ```bash
> > cp ~/unix-course/calculate_pi .
> > file calculate_pi
> > chmod u+x calculate_pi
> > ./calculate_pi
> > ```
> {: .solution}
>
{: .challenge}


#### **05 - Running in background and saving output**

We would like to save the results of the pi calculation program to a file instead of just displaying them on the screen.

> ## Tasks
> 1. Please run the pi executable again but this time send its output to a file called `pi_results.txt` in the same directory. *(1 command)*
> 2. Open a second terminal and enter a command that allows you to watch the output lines being written to the results file. **Note:** Bear in mind that a new terminal always starts in your home directory. *(2 commands)*
> 3. Stop following the results file. *(1 key combination)*
> 
> > ## Solution
> > ```bash
> > ./calculate_pi > pi_results.txt 
> > cd pi_calculation
> > tail -f pi_results.txt
> > # Ctrl+c
> > ```
> {: .solution}
>
{: .challenge}


#### **06 - Inspecting and terminating a running program**

The pi approximation will probably run for about an hour but we would like to terminate it earlier.

> ## Tasks
> 1. List your own running programs. *(1 command)*
> 2. Use the process ID (PID) of the still running pi calculation to terminate it. The PID is in the first column of the program list. *(1 command)*
> 3. Verify that the pi calculation has stopped. *(1 command or action)*
> 4. Inspect the contents of the results file that the pi calculation has generated. *(1 command)*
> 5. Check the file size of the results file. *(1 command)*
> 6. Check the free disk space available on your file system. *(1 command)*
>
> 
> > ## Solution
> > ```bash
> > ps -x
> > kill <id of the process>
> > ps -x     # or look at the first terminal
> > less pi_results.txt
> > ls -lh
> > df -h .
> > ```
> {: .solution}
>
{: .challenge}