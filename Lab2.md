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
josephwhiteman@Josephs-MacBook-Pro-3 ~/wavelet $ javac Server.java ChatServer.java
josephwhiteman@Josephs-MacBook-Pro-3 ~/wavelet $ java ChatServer 4000
Server Started!
```
## Interaction 1: jpolitz’s Greeting
After I launched my ChatServer on port 4000, the first user, jpolitz, sent a greeting:
+ URL Accessed: /add-message?s=Hello&user=jpolitz
+ Method Called: My handleRequest(URI url) method in the Handler class got to work.
+ Arguments I Handled: I passed the handleRequest method a URI url with the value new URI("/add-message?s=Hello&user=jpolitz").
+ Changes in My Fields: My chatMessages string, initially an empty canvas, now captured “jpolitz: Hello\n”.
![alt text](image.jpg)
##Interaction 2: yash’s Question
Not long after, yash joined the chat, adding to the conversation:
+ URL Accessed: /add-message?s=How are you&user=yash
+ Method Called: Once more, handleRequest(URI url) in my Handler class was up for the task.
+ Arguments I Handled: The URI url was provided with new URI("/add-message?s=How are you&user=yash").
+ Changes in My Fields: My chatMessages string now included “jpolitz: Hello\nyash: How are you\n”.
![alt text](image.jpg)
In each of these exchanges, the handleRequest method diligently parses the incoming request’s URL, teases apart the user and message details, and meticulously updates the chatMessages field to reflect the ongoing conversation. This field acts as a living record, charting the ebb and flow of our server’s dialogues.
## Part 2: SSH Key Management and Remote Access
## Generating SSH Keys
+ I started by opening a terminal on my system and running the ssh-keygen command to generate a new pair of SSH keys.During the process, I was prompted to specify the file location for the keys. I chose to save them in the default location (~/.ssh/id_rsa for the private key and ~/.ssh/id_rsa.pub for the public key).I decided to skip setting a passphrase for simplicity, though it’s an option for additional security.The command successfully created my identification and public key, displaying the key’s fingerprint and a randomart image for visual identification of the key.
```
josephwhiteman@Josephs-MacBook-Pro-3 ~ % ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/josephwhiteman/.ssh/id_rsa): 
/Users/josephwhiteman/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/josephwhiteman/.ssh/id_rsa
Your public key has been saved in /Users/josephwhiteman/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:tvEJok+65pRLRTBMf4YAwBHtED01Xp1EpObK0PHfayM josephwhiteman@Josephs-MacBook-Pro-3.local
The key's randomart image is:
+---[RSA 3072]----+
|o=B+*o .=+.      |
| o +o=o..o       |
|  o .o+oo        |
|   ...=o         |
|   . .ooS        |
|    o+.o.=..     |
|    =o. ..o.     |
|   o.=   E o.    |
|   o=..   o..    |
+----[SHA256]-----+
```
## Locating the SSH Keys
+ Next, I wanted to confirm the existence and location of my newly generated SSH keys.I used the ls -l ~/.ssh/id_rsa command to display details about my private key, confirming its presence in my .ssh directory. I also ran ls -l ~/.ssh/ to list all files in my .ssh directory, where I found the id_rsa (private key), id_rsa.pub (public key), and the known_hosts file. Blthej
```
josephwhiteman@Josephs-MacBook-Pro-3 ~ % ls -l ~/.ssh/id_rsa
-rw-------  1 josephwhiteman  staff  2635 Apr 24 17:00 /Users/josephwhiteman/.ssh/id_rsa
josephwhiteman@Josephs-MacBook-Pro-3 ~ % ls -l ~/.ssh/
total 40
-rw-r--r--  1 josephwhiteman  staff    63 Apr 16 15:40 config
-rw-------  1 josephwhiteman  staff  2635 Apr 24 17:00 id_rsa
-rw-r--r--  1 josephwhiteman  staff   596 Apr 24 17:00 id_rsa.pub
-rw-------  1 josephwhiteman  staff   272 Apr  9 15:26 known_hosts
-rw-r--r--  1 josephwhiteman  staff    96 Apr  9 15:26 known_hosts.old
josephwhiteman@Josephs-MacBook-Pro-3 ~ %
```
## Copying Public Key to Remote Server
+ With my public key ready, I used the scp command to securely copy it to the authorized_keys file on the remote server (ieng6 in this case).After entering my password, the public key was successfully transferred to the remote server’s ~/.ssh/authorized_keys file.
```
josephwhiteman@Josephs-MacBook-Pro-3 ~ % ssh-copy-id -i ~/.ssh/id_rsa.pub jwhiteman@ieng6.ucsd.edu 
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/josephwhiteman/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
(jwhiteman@ieng6.ucsd.edu) Password: 

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'jwhiteman@ieng6.ucsd.edu'"
and check to make sure that only the key(s) you wanted were added.
```
## SSH into Remote Server Without a Password
+ Finally, I tested SSH access to the ieng6 server using my newly set up SSH keys.I ran ssh 'jwhiteman@ieng6.ucsd.edu' and was able to log in without being prompted for a password, thanks to the SSH key authentication.Upon logging in, I was greeted with the server’s welcome message and some system status information.
```
josephwhiteman@Josephs-MacBook-Pro-3 ~ % ssh 'jwhiteman@ieng6.ucsd.edu'
Last login: Tue Mar 12 19:49:24 2024 from 076-033-215-103.inf.spectrum.com
Hello jwhiteman, you are currently logged into ieng6-202.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   17:10:01   21  0.10,  0.32,  0.41
ieng6-202   17:10:01   21  1.99,  1.76,  1.24
ieng6-203   17:10:01   20  0.98,  1.21,  1.47

 

To begin work for one of your courses [ cs15lsp24 ], type its name 
at the command prompt.  (For example, "cs15lsp24", without the quotes).

To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options.
[jwhiteman@ieng6-202]:~:95$
```
## Part 3: Learning Outcomes from Recent Labs
In these past labs, I learnt how to set up and maintain a Java-based chat server on a remote server. This includes an understanding of how many users can talk with the server at the same time. I also had practical experience using SSH keys for secure and convenient remote server access, eliminating the need for password authentication. This knowledge is useful for effectively and securely administering remote servers and applications.
