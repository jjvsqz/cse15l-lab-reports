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
