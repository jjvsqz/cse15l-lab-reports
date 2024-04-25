# Lab Report 2
## Header: *Juan Junior Vasquez_A17536681_CSE 15L Week #4: 04/22/2024 - 04/26/2024*
## Part 1: ChatServer Interactions
Welcome to Lab Report 2, where we dive into the intricacies of our ChatServer’s interactions, tracking the flow of messages and observing the underlying mechanics of our Java server in action.
## Code:
```
import java.io.IOException;
import java.net.URI;
class ChatHandler implements URLHandler {
    // The state of the server: a StringBuilder to accumulate chat messages
    StringBuilder chatHistory = new StringBuilder();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return chatHistory.length() == 0 ? "No messages yet." : chatHistory.toString();
        } else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String user = null;
            String message = null;
            for (String param : parameters) {
                String[] keyValue = param.split("=");
                if (keyValue[0].equals("user")) {
                    user = keyValue[1];
                } else if (keyValue[0].equals("s")) {
                    message = keyValue[1];
                }
            }

            if (user != null && message != null) {
                chatHistory.append(user).append(": ").append(message).append("\n");
                return chatHistory.toString(); // Return the updated chat history
            } else {
                return "Invalid request. User and message parameters are required.";
            }
        } else {
            return "404 Not Found!";
        }
    }
}
class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new ChatHandler());
    }
}
```
I’m also using Server.java, which is provided in previous labs. After I run following code

```
{
juanj@BOOK-CJCG9LS1GL ~ % cd Desktop/lab1
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % 
}
```
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL. Upon executing the cd command, there is no visible output, but the command effectively changes the working directory to /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1. This outcome is in line with the expected behavior of the cd command, which is designed to switch the working directory to the specified location. No errors were encountered during the execution of the command.
## 3. cd with a file as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % cd Hello.java
bash: cd: Hello.java: Not a directory
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % 
}
```
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1. Upon attempting to execute the cd command with the argument Hello.java, an error message is generated. This error occurs because the cd command expects a directory as its argument, not a file. The attempted navigation into Hello.java as if it were a directory is not possible. Therefore, the command fails, resulting in an error.
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
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1. Upon executing the ls command without any arguments, the output displays the contents of the current working directory, which include Hello.java and README.md. This behavior aligns with the functionality of the ls command, as it lists all files and directories in the current directory when executed without any arguments. No errors were encountered during the execution of the command.
## 2. ls with a directory as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~ % ls Desktop/lab1
Hello.java   README.md
juanj@BOOK-CJCG9LS1GL ~ % 
}
```
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL. When executing the ls command with the argument Desktop/lab1, the output displays the contents of the directory Desktop/lab1, revealing the same files as mentioned previously. This behavior aligns with the intended functionality of the ls command, which is to list the contents of the specified directory. No errors occurred during the execution of the command.
## 3. ls with a file as an argument
```
{
juanj@BOOK-CJCG9LS1GL-MBP-3 ~/Desktop/lab1 % ls Hello.java
Hello.java
juanj@BOOK-CJCG9LS1GL-MBP-3 ~/Desktop/lab1 % 
}
```
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1. Executing the ls command with the argument Hello.java results in the output displaying the specified file, Hello.java. This outcome aligns with the expected behavior of the ls command when used with a file as an argument, as it verifies the existence of the file and displays its name. No errors were encountered during the execution of the command.
## The cat Command
The cat command is used to display the contents of a file.
## 1. cat with no argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop/lab1 % cat
^Z
}
```
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1. Upon executing the cat command without any arguments, the output indicates that the command waits for input from the user. This behavior is expected, as cat without an argument indeed waits for input from the terminal. No errors were encountered during this process, as it is a standard functionality of the cat command.
## 2. cat with a directory as an argument
```
{
juanj@BOOK-CJCG9LS1GL ~/Desktop % cat lab1
cat: lab1: Is a directory
}
```
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL/Desktop, executing the cat command with the argument lab1 results in an error message. This error occurs because cat expects a file as its argument, not a directory. The attempt to use cat on a directory leads to an error because cat is specifically designed to display the contents of files, not directories. Therefore, the error message is generated as lab1 is identified as a directory, not a file.
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
The initial directory is /Users/juanj@BOOK-CJCG9LS1GL/Desktop/lab1, executing the cat command results in the output displaying the contents of the file Hello.java. This behavior aligns with the expected functionality of the cat command, which is designed to display the contents of specified files. No errors occurred during the execution of the command, as it successfully displayed the contents of the Hello.java file.
