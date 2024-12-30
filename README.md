# CTF-Bandit 🦝
Writeup of how I solved each level of OverTheWire's Wargame: Bandit. 

# Objective 👾
This wargame is meant to teach more technical and practical skills. You learn how to authenticate over a network through SSH, and gain familiarity with the CMD Line. This CTF game is meant for absolute beginners, and it has greatly helped me in getting more comfortable with a terminal, as well as given the added benefit of allowing me to very briefly come up with my own methodologies.

### Level 0
Level Goal: Log into the game using SSH (A remote login client)

Note: An SSH Client is a program for logging into a remote machine and for executing commands on a remote machine. It's intended to provide secure encrypted communications between two untrusted hosts over an insecure network.

Most notable applications are remote login and command-line execution.

  1. Download Cygwin (Use wikihow)
  2. Use ssh to log into Bandit (Used Linux manual page for help)
     - `$ ssh bandit0@bandit.labs.overthewire.org -p 2220`
  3. It MIGHT ask if you'd like to continue connecting. Type 'Yes' or 'y', then press enter.
  4. Put the password (it's given to you already).
 

### Level 0 -> Level 1
Level goal: Find password for the next level. (Stored in a file called readme)

Note:  In a SSH (Secure Shell), you typically use command-line tools to navigate the file system and view files.

<details><summary>✨Here are some common commands you can use to view files in SSH✨</summary>
<p>
  
*  `ls` -> The `ls` command lists files and directories in the current directory. You can use it without any arguments to list the files in the current directory.
  *  `ls -l` -> to list files in long format that includes more detailed information like permissions, owner, size, and modification date, you can use the `-l` option.
  *  `cat` -> the `cat` command is used to display the contents of a file. you can use it like this:
    - `cat` filename
  * `more` or `less` -> if a file is too long to display on one screen, you can use it `more` or `less` to view it page by page.
      - `more` filename
      - `less` filename
  * `head` -> to display the first few lines of a file, you can use the `head` command.
  * `tail` -> to display the last few lines of a file, you can use the `tail` command.
  * `vi` or `nano` -> if you want to view or edit a file, you can use text editors  like `vi` or `nano`.

</p>
</details>
  
1. After logging into Level 0, you'll use this level to find the password for level 1.
     - You can use the `ls` command to list the files in directory. then use `cat` command to view what's inside the file. The password should be in that file.
     - `$ ls`
     - `$ cat filemane`
2. Switch to the next level (bandit1)
     * You'll need to exit Level 0, you do this by using the `ctrl -d` command.
     * Then, log into Level 0 the same way you did level 0, but use the username bandit1 instead of bandit0.
       - `ssh bandit1@bandit.labs.overthewire.org -p 2220` (make sure to stay in the same port).
3. Now you enter the password you found in step 1 to log into this level.
 

### Level 1 -> Level 2
Level goal: The password for the next level is in a file called `-` located in the home directory.

1. Google search 'dashed filename'
   - This type of approach has a lot of misunderstandings because using `-` as an argument refers to STDIN/STDOUT i.e. dev/stdin or dev/stdout. So, if you want to open this file you have to specify the full location of the file such as `./-`
   - For e.g., if you want to see what's inside the file use: `cat ./-`.
  

### Level 2 -> Level 3
Level goal: the password is stored in a file called `spaces in this filename` located in the home dorectory.

1. Google search 'spaces in filename'.
   - Normally, filenames don't contain spaces in them since usually we'd see underscores in file or directory names. And it's not that you can't use spaces in a filename, it's just that it creates additional pain and you should avoid it if possible.
   - There are two ways to deal with spaces in a filename:
     1) Wrap the entire filename between quotes:
          - `"filename with spaces"` (you can choose either single or double quotes, it doesn't matter which one besides making it look more organized)
     2) Escape everyspace using backslash key:
        - `file\ name\ with\ spaces\`
2. Here, I just used `cat "spaces in this filename` to look into the file and retrieve the password for level 3 (bandit3).

### Level 3 -> Level 4
Level goal: Password is stored in a hidden file in the `inhere` directory.

1. `$ ls` - will list/show the inhere directory.
2. `$ cd inhere` - switching to the inhere directory.
   - The `ls` command won't be useful in this directory. Use the `find` command to list out the hidden files in the inhere directory.
   - Use the `cat` command to look into the hidden files, and you should find level 4's password in one of them.


### Level 4 -> Level 5
Level goal: The password for the next level is stored in the only human-readable file in the inhere directory. TIP: if your terminal is messed up, try the `reset` command.

<details><summary>✨Human Readable Text Format✨</summary>
<p>

Human readable text is a text that is written in ASCII format or a format readable to humans and not data or any binary format.

The `file` command is used to determine the type of file. `.file` type may be of human-readable (e.g. 'ASCII Text') or MIME type (e.g. 'text/plain; charset = us-ascii'). This command tests each argument in an attempt to categorize it.

Examples:
  * `file [option][filename]`
  * `file -b filename`
  * `file *`
  * `file directoryname/*`

 1) `-b`, `-brief` : this is used to display just file type in brief mode.
 2) `*` option : command displays the all file's file type.
 3) `directoryname/*` option : This is used to display all files filetype in particular directory.
  
</p>
</details>

1. Use `ls` command
2. Then use `file inhere/*` command to list all files in directory.
   - you'll see one file that is human-readable (bcuz of ASCII).
3. Use `cat` command to look into file and get password.
     - `$ cat inhere/-file07`


### Level 5 -> Level 6



