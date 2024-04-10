# Lab Report 1: Exploring Basic Filesystem Commands
## Introduction: *In this lab report, we delve into the foundational aspects of navigating and manipulating the filesystem via the command line interface. Central to our exploration are three pivotal commands: 'cd' for directory navigation, 'ls' for directory listing, and 'cat' for file content display. By leveraging examples from our lab workspace, we aim to illustrate the functionality and outcomes of each command with and without arguments, offering comprehensive insights into their operation.*
## The cd Command
## 1. cd with no argument
```
{
juanj@BOOK-CJCG9LS1GL ~ % cd
juanj@BOOK-CJCG9LS1GL ~ %
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL
* Output: No visible output; the command changes the working directory to the user’s home directory.
* Explanation: The cd command without arguments defaults to the user’s home directory.
* Error: No Error
## 2. cd with a directory as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~ % cd Desktop/lab1
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % 
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL
* Output: No visible output; the command changes the working directory to /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1.
* Explanation: The cd command changes the working directory to the specified directory.
* Error: No Error
## 3. cd with a file as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % cd Hello.java
bash: cd: Hello.java: Not a directory
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % 
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1
* Output: Error message because cd expects a directory as its argument, not a file.
* Explanation: The command attempted to navigate into a file as if it were a directory, which is not possible.
* Error: Yes, the command fails because Hello.java is a file, not a directory.
## The ls Command
The ls command lists the files and directories within a directory.
## 1. ls with no argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % ls
Hello.java   README.md
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % 
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1
* Output: Lists the contents of the current working directory (Hello.java and README.md).
* Explanation: ls with no arguments lists all files and directories in the current directory.
* Error: No Error
## 2. ls with a directory as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~ % ls Desktop/lab1
Hello.java   README.md
juanj@BOOK-CJCG9LS1GL ~ % 
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL
* Output: Lists the contents of Desktop/lab1, showing the same files.
* Explanation: ls lists the contents of the specified directory.
* Error: No Error
## 3. ls with a file as an argument
```
{
juanj@BOOK-CJCG9LS1GL-MBP-3 ~/Desktop/lab1 % ls Hello.java
Hello.java
juanj@BOOK-CJCG9LS1GL-MBP-3 ~/Desktop/lab1 % 
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1
* Output: Displays the specified file (Hello.java).
* Explanation: When ls is used with a file as an argument, it verifies the existence of the file and displays its name.
* Error: No Error
## The cat Command
The cat command is used to display the contents of a file.
## 1. cat with no argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % cat
^Z
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1
* Output: Waits for input from the user.
* Explanation: cat without an argument waits for input from the terminal.
* Error: No Error
## 2. cat with a directory as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop % cat lab1
cat: lab1: Is a directory
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL/Desktop
* Output: Error message, as cat expects a file, not a directory.
* Explanation: Attempting to use cat on a directory results in an error because cat is designed to display the contents of files.
* Error: Yes, because lab1 is a directory, not a file.
## 3. cat with a file as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % cat Hello.java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 %
}
```
* Initial directory: /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1
* Output: Displays the contents of Hello.java.
* Explanation: cat displays the contents of the specified file.
* Error: No Error
