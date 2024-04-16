## Part 1, ChatServer


ChatServer code:
```
import java.io.IOException;
import java.net.URI;

class Handler3 implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String log = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return log;
        } 
        else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] message = parameters[0].split("=");
            String[] user = parameters[1].split("=");

            if (message[0].equals("s") && user[0].equals("user")) {
                log += user[1] + ": " + message[1] + "\n";

                return log;
            }
        }
        return "404 Not Found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler3());
    }
}
```

Screenshots:
![image](ChatServer1.png)
![image](ChatServer2.png)
