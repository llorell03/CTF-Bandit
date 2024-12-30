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

 🌱TIP: To copy & paste in cygwin, just highlight the text and then right click where it asks for the password. (You won't be able to see the password, it will be invisible).

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
   - 🌱 The `ls` command won't be useful in this directory. Use the `find` command to list out the hidden files in the inhere directory.
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

1. Use `ls` command.
   - 🌱 I thought about using `cd inhere` to enter the directory, then used `find` to look at the files, but it didn't help. Used `cd -` to back out of current directory. 
3. Use `file inhere/*` command to list all files in directory.
   - you'll see one file that is human-readable (bcuz of ASCII).
4. Use `cat` command to look into file and get password.
     - `$ cat inhere/-file07`


### Level 5 -> Level 6
Level goal: The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
* human-readable
* 1033 bytes in size
* not executable

1. SO, I decided to try googling how to find files that are a certain number of bytes. I found using `find -size [...]` would allow me to find the correct file(s) with that specific size in bytes.
   - `find -size 1033c`
      <details><summary>✨ Why did I use '1033c' and not just '1033'? Check the `man` page ✨</summary>
      <p>
        
                 -size n[cwbkMG]
        
                        File uses n units of space, rounding up.  The following suffixes can be used:
        
                        `b`    for 512-byte blocks (this is the default if no suffix is used)
     
                        `c`    for bytes
     
                        `w`    for two-byte words
     
                        `k`    for Kilobytes (units of 1024 bytes)
     
                        `M`    for Megabytes (units of 1048576 bytes)
     
                        `G`    for Gigabytes (units of 1073741824 bytes) 
      </p>
      </details>
2. To check if it was not executable I used `! -executable` command.
   - `$ find -size 1033c ! -executable`.
3. By this time, i firgured this file was the correct one, and I was having a hard time finding the right command to check if it was human-readable. I ended up just using `ls -l` and then `file` command to look at the file to check if it was both human-readable and executable.
   
            bandit5@bandit:~$ ls -l ./inhere/maybehere07/.file2
            -rw-r----- 1 root bandit5 1033 May  7 20:15 ./inhere/maybehere07/.file2           
            bandit5@bandit:~$           
            bandit5@bandit:~$ file ./inhere/maybehere07/.file2           
            ./inhere/maybehere07/.file2: ASCII text, with very long lines           
            bandit5@bandit:~$ 

    * human-readable (ASCII text)
    * 1033 bytes in size (Also in `ls -l` output)
    * not executable (`-rw-r-----`)
5. I then just used `cat` to look into that file and it gave me the password.


### Level 6 -> Level 7
Level goal: The password for the next level is stored somewhere on the server and has all of the following properties:

 * owned by user bandit7
 * owned by group bandit6
 * 33 bytes in size

1. In the previous level, I learned that the `find` command can be used to find files on the server. Using the `man` page (and using ctrl + f), I saw it offers flags to look for files owned by a specific user (`-user <username>`) and a specific group (`group <groupname>`).
    * -type f,  because we are looking for a file
    * -user bandit7, to find files owned by the ‘bandit7’ user
    * -group bandit6, to find files owned by the ‘bandit6’ group
    * -size 33c, to find files of size 33 bytes

 `$ find / -type f -user bandit7 -group bandit6 -size 33c`

    
2. We would need to run the command from the root directory to search the whole system. However, running this command will print out the `Permission denied` error. I google searched 'How to get rid of all "permission denied" messages in "find"?', I found using `2>/dev/null` fixes that problem.
   - `$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`
4. Once I used that command, it revealed the file and I just used the `cat` command to show the password.
