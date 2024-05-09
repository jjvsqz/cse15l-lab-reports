# Lab Report 3
## Part 1: ChatServer Interactions
In Lab Report 2, we delve deep into the complexities of our ChatServer's interactions, meticulously tracing the path of messages and examining the fundamental mechanics of our Java server in operation.
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
## End of Code

```
PS C:\User\juanj ~/wavelet $ javac Server.java ChatServer.java
PS C:\User\juanj ~/wavelet $ java ChatServer 4000
Server Started!
```
I utilized the Server.java file in the pervious step

## Interaction 1: The Greeting
Upon launching my ChatServer on port 4000, the initial user, jpolitz, greeted:
Upon accessing the URL ```"/add-message?s=Hello&user=jpolitz"```, the system triggered the execution of the ```handleRequest(URI url)``` method within the ```Handler``` class. This method was invoked with the argument of a URI url, specifically new URI```("/add-message?s=Hello&user=jpolitz")```. Subsequently, within this method, I managed the processing of the provided URI, resulting in an update to the chatMessages field. Initially void, the chatMessages string now encapsulates the message ```"jpolitz: Hello\n"```.

## Interaction 2: Question
Shortly thereafter, yash joined the conversation, contributing with:
Upon accessing the URL ```"/add-message?s=Hello&user=jpolitz"```, the system activated my handleRequest(URI url) method within the ```Handler``` class. I handled the method with a URI url parameter, instantiated as new URI```("/add-message?s=Hello&user=jpolitz")```. This processing resulted in an update to the ```chatMessages``` string, which was initially empty but now contains the message "jpolitz: Hello\n".

## Part 2: Generating SSH Keys and Remote Access
I began by initiating a terminal session on my system and executing the ssh-keygen command to produce a fresh set of SSH keys. Throughout the procedure, I was prompted to designate the file location for these keys. Opting for convenience, I elected to store them in the default directory (```~/.ssh/id_rsa``` for the private key and ```~/.ssh/id_rsa.pub``` for the public key). In the interest of simplicity, I chose to forgo setting a passphrase, although it remains an option for heightened security. The command completed successfully, generating my identification and public key, along with displaying the key's fingerprint and a randomart image for visual verification.
```
PS C:\User\juanj> ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/juanj/.ssh/id_rsa): 
/Users/juanj/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/juanj/.ssh/id_rsa
Your public key has been saved in /Users/juanj/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:0mP7NzXpV+AVzatXYcAO+pIRINCp9gdmcK8RfihDWE juanj@BOOK-CJCG9LS1GL
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
## Locating
Following that, I sought to verify the presence and location of my freshly generated SSH keys. Utilizing the ```ls -l ~/.ssh/id_rsa``` command, I accessed details regarding my private key, affirming its existence within my ```.ssh``` directory. Additionally, I executed ```ls -l ~/.ssh/``` to enumerate all files in my ```.ssh``` directory, identifying the ```id_rsa``` (private key), ```id_rsa.pub``` (public key), and the ```known_hosts``` file.

```
PS C:\User\juanj> ls -l ~/.ssh/id_rsa
-rw-------  1 juanj  staff  2635 Apr 24 17:00 /Users/juanj/.ssh/id_rsa
PS C:\User\juanj> ls -l ~/.ssh/
total 40
-rw-r--r--  1 juanj  staff    63 Apr 16 15:40 config
-rw-------  1 juanj  staff  2635 Apr 24 17:00 id_rsa
-rw-r--r--  1 juanj  staff   596 Apr 24 17:00 id_rsa.pub
-rw-------  1 juanj  staff   272 Apr  9 15:26 known_hosts
-rw-r--r--  1 juanj  staff    96 Apr  9 15:26 known_hosts.old
PS C:\User\juanj>
```

## Copying to Remote Server
With my public key, I employed the ```scp``` command to securely transfer it to the authorized_keys file on the remote server (ieng6 in this instance). Following password authentication, the public key was effectively conveyed to the ```~/.ssh/authorized_keys``` file on the remote server.

```
PS C:\User\juanj> ssh-copy-id -i ~/.ssh/id_rsa.pub jjv001@ieng6.ucsd.edu 
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/juanj/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
(jjv001@ieng6.ucsd.edu) Password: 

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'jjv001@ieng6.ucsd.edu'"
and check to make sure that only the key(s) you wanted were added.
```

## SSH into Remote Server Without a Password
In the final step, I verified SSH access to the ieng6 server using my freshly configured SSH keys. Executing ssh ```'jjv001@ieng6.ucsd.edu'```, I successfully logged in without encountering a password prompt, owing to SSH key authentication. Upon access, I was welcomed with the server's message and provided with system status updates.

```
PS C:\User\juanj> ssh 'jjv001@ieng6.ucsd.edu'
Last login: Tue May 23 19:48:27 2024 from 076-033-215-103.inf.spectrum.com
Hello juanj, you are currently logged into ieng6-201.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   15:35:21   9  0.89,  0.90,  0.69
ieng6-202   15:35:21   13  1.99,  1.76,  1.24
ieng6-203   15:35:21   17  5.07,  5.21,  5.49

 

To begin work for one of your courses [ cs15lsp24 ], type its name 
at the command prompt.  (For example, "cs15lsp24", without the quotes).

To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options.
[jjv001@ieng6-201]:~:94$
```

## Part 3: Learning Outcomes from Recent Labs
Throughout previous labs, I acquired the skills to e
