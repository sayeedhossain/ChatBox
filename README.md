# ChatBox
This is an android base/terminal base ChatBox.Actually this is designed in same network for p2p or g2g communication.

1)server.java - command line based server that works as intermediate between two clients by receiving data from one sender and broadcasting it to all other receivers connected to the server
2)client.java - Java swing GUI program that runs on each independent client and is connected to the server program running on a terminal window.

Server Side Programming(Server.java)

Server class : The main server implementation is easy and similar to the previous article. The following points will help understand Server implementation :
The server runs an infinite loop to keep accepting incoming requests.
When a request comes, it assigns a new thread to handle the communication part.
The sever also stores the client name into a vector, to keep a track of connected devices. The vector stores the thread object corresponding to the current request. The helper class uses this vector to find the name of recipient to which message is to be delivered. As this vector holds all the streams, handler class can use it to successfully deliver messages to specific clients.
Invoke the start() method.
 

ClientHandler class : Similar to previous article, we create a helper class for handling various requests. This time, along with the socket and streams, we introduce a name variable. This will hold the name of the client that is connected to the server. The following points will help understand ClientHandler implementation :
Whenever the handler receives any string, it breaks it into the message and recipient part. It uses Stringtokenizer for this purpose with ‘#’ as the delimiter. Here it is assumed that the string is always of the format:
message # recipient
It then searches for the name of recipient in the connected clients list, stored as a vector in the server. If it finds the recipients name in the clients list, it forwards the message on its output stream with the name of the sender prefixed to the message.



Limitations:
Although the above implementation of server manages to handle most of the scenarios, there are some shortcomings in the approach defined above.

One clear observation from above programs is that if the number of clients grew large, the searching time would increase in the handler class. To avoid this increase, two hash maps can be used. One with name as the key, and index in active list as the value. Another with index as key, and associated handler object as value. This way, we can quickly look up the two hashmaps for matching recipient. It is left to the readers to implement this hack to increase efficiency of the implementation.
Another thing to notice is that this implementation doesn’t work well when users disconnect from the server. A lot of errors would be thrown because disconnection is not handled in this implementation. It can easily be implemented as in previous basic TCP examples. It is also left for the reader to implement this feature in the program.

<h4>Any further query? just feel free to contact at (me@sayeedhossain.com) </h4>

