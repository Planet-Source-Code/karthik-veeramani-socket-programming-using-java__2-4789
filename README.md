<div align="center">

## Socket Programming Using Java


</div>

### Description

This tutorial will make you understand what sockets are, and will help you to start coding simple networking applications using Java.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Karthik Veeramani](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/karthik-veeramani.md)
**Level**          |Beginner
**User Rating**    |4.8 (380 globes from 79 users)
**Compatibility**  |Java \(JDK 1\.1\), Java \(JDK 1\.2\), Java \(JDK 1\.3\), Java \(JDK 1\.4\), Java \(JDK 1\.5\)
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__2-57.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/karthik-veeramani-socket-programming-using-java__2-4789/archive/master.zip)





### Source Code

<h2 align="center">SOCKET PROGRAMMING USING JAVA</h2>
<h4 align="center">If you find this tutorial good enough, please vote for me (use the Your Vote! section at the end of this page)</h4>
<p>So you want to start doing some network programming with Java... You've come
 to the right place. I'll introduce you to the
 interesting world of Java sockets. By the end of this tutorial, you should be
 able to understand what sockets are and how to
 build simple Java applications using sockets. </p>
<p><b>Whats a socket?</b></p>
<p> Don't tell me you've never chatted on those instant messengers like yahoo,
 msn and aol. But its OK if you never understood what goes on behind the scene;
 after all, thats what we are here for. Lets say you've installed one of those
 instant messengers on your computer. After you run it and enter your user name
 and password, the messenger tries to <i>connect</i> to its server (say, the
 yahoo server). What exactly does this 'connect' mean? </p>
<p>Every computer on a network has an IP address. This address is like your house
 address, something that identifies your computer
 uniquely, allowing others to communicate with your computer. I wont go much
 into IP addresses, but let me just tell you that an IP
 address looks something like this - 64.104.137.158 - a set of numbers separated
 with dots. However, some computers with rich
 owners will also choose to have a <b>domain name</b> in addition to this sick
 looking number, so that people can easily identify them. A
 domain name looks far more sane - like www.yahoo.com. There are some special
 computers on the Internet, whose sole purpose
 in life is to translate the domain name to IP address and vice versa. </p>
<p>Now, you know that many programs can run on the same computer, don't you? Lets
 say that, there are some 10 programs running
 on a certain computer. To add to the confusion, lets say all of them are waiting
 for other computers to contact them. Imagine it like
 this - 10 of you share a big office space and a single telephone - and all of
 you expect calls from your own clients. How will you handle
 this? Perhaps appoint one person who'll hand over the call to the right person.
 Possible, but an undeniable menace. This will mean,
 when one of you take the call, other clients will not be able to reach the rest
 of you. Besides, its a pain to have a person route the calls
 to the right people. You must have guessed what I'm heading at - if all those
 programs running on a single computer proudly ask their
 clients to contact them on a certain IP address, their clients are not going
 to be pleased. The idea is... having a separate IP address per
 program, right? WRONG. Thats out of question. Its like asking for a separate
 office for each of you. Wont separate phone numbers
 suffice? Yes. In networking parlance, we call these 'separate phone numbers'
 as ports. A port is just a simple number - each program
 running on the same computer can choose to have a unique port number to identify
 itself to the outside world. REMEMBER - these
 ports are not slots on your computer hardware - dont think you can find them
 if you try hard enough. They are just logical numbers. Now
 the point should be clear. We have an IP address that lets the other computers
 look for a certain computer on the network. And we have
 a port number that'll identify a certain program running on that computer. Understand
 that, two programs running on different computers
 CAN use the same port number. Two houses on different streets can have the same
 house number, can't they? So, finally, we are almost
 there - just to scare you a bit, lets derive a formula -</p>
<p>An IP address = uniquely identifies a computer on the network.
 A port number = uniquely identifies a program running on a computer.</p>
<p>Adding the above equations,</p>
<p>An IP address + A port number = _______</p>
<p>In other words,
 A _____ = uniquely identifies a program on the network</p>
<p>If you guessed it right, thanks, my effort didn't go waste. If you didn't,
 no problem, go back and read from the beginning, or google for a
 better tutorial. The ____ is... <b>SOCKET</b>!</p>
<p>
 To summarize, a socket is a combination of an IP address and a port. A socket
 address lets other computers on the network locate a
 certain program running on a certain computer. You may represent a socket address
 like 64.104.137.58:80, where 64.104.137.58 is
 the IP address and 80 is the port number.</p>
<p><b>How to program</b> </p>
<p>Enough of theory talk. Lets get into some action now. We are going to write
 some very simple Java code, that'll demonstrate the use of sockets. Here is
 what is going to happen - </p>
<p>1) One Java program will try to connect to another Java program (which is desperately
 waiting for someone to contact it). Lets call the
 first program as Client, and the second as Server.
 <br>2) Once connected, the client program is going to accept whatever you type,
 and send it dutifully to the server program.
 <br>3) The server is going to send back the same text to the client, just to show
 that it is least interested in doing such an uninteresting thing.
 <br>4) The client, after getting back the same text from the server, is going to
 throw it on your face, showing you what the server thinks about
 you.</p>
<p>Ready? Lets get started. Note that, I wont be teaching you Java programming
 from scratch, I'll explain only the socket-related portions
 of the code.</p>
<p>Create 2 fresh Java programs and call them Server.java and Client.java. I'll
 paste the code below, but don't be scared, I'll explain.</p>
<b>Server.java</b>
<pre>
import java.net.*;
import java.io.*;</pre>
<pre>public class Server {</pre>
<pre>public static void main(String[] ar) {</pre>
<pre> int port = 6666; // just a random port. make sure you enter something between 1025 and 65535.</pre>
<pre> try {
 ServerSocket ss = new ServerSocket(port); // create a server socket and bind it to the above port number.
 System.out.println("Waiting for a client...");</pre>
<pre> Socket socket = ss.accept(); // make the server listen for a connection, and let you know when it gets one.</pre>
<pre> System.out.println("Got a client :) ... Finally, someone saw me through all the cover!");
 System.out.println();</pre>
<pre> // Get the input and output streams of the socket, so that you can receive and send data to the client.
 InputStream sin = socket.getInputStream();
 OutputStream sout = socket.getOutputStream();</pre>
<pre> // Just converting them to different streams, so that string handling becomes easier.
 DataInputStream in = new DataInputStream(sin);
 DataOutputStream out = new DataOutputStream(sout);</pre>
<pre> String line = null;
 while(true) {</pre>
<pre> line = in.readUTF(); // wait for the client to send a line of text.</pre>
<pre> System.out.println("The dumb client just sent me this line : " + line);
 System.out.println("I'm sending it back...");</pre>
<pre> out.writeUTF(line); // send the same line back to the client.
 out.flush(); // flush the stream to ensure that the data reaches the other end.</pre>
<pre> System.out.println("Waiting for the next line...");
 System.out.println();
 }
 } catch(Exception x) {
 x.printStackTrace();
 }
 }
 }
 </pre>
<b>Client.java</b>
<pre>
import java.net.*;
import java.io.*;</pre>
<pre>public class Client {</pre>
<pre>public static void main(String[] ar) {</pre>
<pre> int serverPort = 6666; // make sure you give the port number on which the server is listening.
 String address = "127.0.0.1"; // this is the IP address of the server program's computer. // the address given here means "the same computer as the client".</pre>
<pre>
 try {
 InetAddress ipAddress = InetAddress.getByName(address); // create an object that represents the above IP address.
 System.out.println("Any of you heard of a socket with IP address " + address + " and port " + serverPort + "?");</pre>
<pre> Socket socket = new Socket(ipAddress, serverPort); // create a socket with the server's IP address and server's port.
 System.out.println("Yes! I just got hold of the program.");</pre>
<pre> // Get the input and output streams of the socket, so that you can receive and send data to the client.
 InputStream sin = socket.getInputStream();
 OutputStream sout = socket.getOutputStream();</pre>
<pre> // Just converting them to different streams, so that string handling becomes easier.
 DataInputStream in = new DataInputStream(sin);
 DataOutputStream out = new DataOutputStream(sout);</pre>
<pre> // Create a stream to read from the keyboard.
 BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));</pre>
<pre> String line = null;
 System.out.println("Type in something and press enter. Will send it to the server and tell ya what it thinks.");
 System.out.println();</pre>
<pre> while(true) {
 line = keyboard.readLine(); // wait for the user to type in something and press enter.</pre>
<pre> System.out.println("Sending this line to the server...");
 out.writeUTF(line); // send the above line to the server.
 out.flush(); // flush the stream to ensure that the data reaches the other end.
 line = in.readUTF(); // wait for the server to send a line of text.</pre>
<pre> System.out.println("The server was very polite. It sent me this : " + line);
 System.out.println("Looks like the server is pleased with us. Go ahead and enter more lines.");
 System.out.println();
 }
 } catch(Exception x) {
 x.printStackTrace();
 }
 }
 }
 </pre>
Compile it with <br>
<pre> javac Server.java Client.java </pre>
Open two command windows (DOS prompts). In one of those, enter<br>
<pre> java Server</pre>
and in the other,<br>
<pre> java Client</pre>
<p>(in that order!)</p>
<p>Type something on the client window and press enter. Observe both windows and
 see what happens. Finally, press ctrl-C to kill the programs.</p>
<p><b>Explanation</b> </p>
<p>Lets delve into the code now. You must have got some idea looking at the comments,
 still, lets try to analyze a few critical lines.</p>
<p>The server code has the lines</p>
<p>ServerSocket ss = new ServerSocket(port);<br>
 Socket socket = ss.accept();</p>
<p>A ServerSocket class is slightly different from the Socket class. The Socket
 class is exactly what you think.. well, it represents a
 socket. The ServerSocket class is mainly for allowing a program to <i>listen</i> for
 connections from clients. You create it by assigning it a
 port number on which it can work on. Once created, you need to call its accept()
 method. This method will make the program
 listen on the given port for connections. It hangs there until it gets a client.
 Once a client gets in touch, it creates a normal Socket
 object, and hands it over to you so that you can start doing all the socket
 operations you want. Note that, this Socket object
 returned by accept() method, represents the other end of the connection. After
 all, if you want to send some data to the client,
 you can't write it to your own socket!</p>
<p>Next is the Socket class. You create the Socket object by passing an IP address
 and a port number. Java gives you the
 InetAddress class to represent an IP address, so you better go their way and
 use it. To create an InetAddress object that
 represents an IP address, you can use this method -</p>
<p>InetAddress ipAddress = InetAddress.getByName(address);</p>
<p>Note that in our program, we have 127.0.0.1 for the address. This address is
 a special address called <i>loopback</i> address.
 Don't panic, it is just an address that represents the local computer. If you
 intend to run the client and server on different
 machines, use the correct IP address of the server.</p>
<p>Once the InetAddress is created, we create the Socket,
 Socket socket = new Socket(ipAddress, serverPort);</p>
<p>Once you have the Socket object, you can get the input and output streams of
 the socket. The input stream will let you
 read from the socket and the output stream lets you write to the socket. </p>
<p>InputStream sin = socket.getInputStream();
 OutputStream sout = socket.getOutputStream();</p>
<p>The below lines are just for converting the above to different types of streams.
 So that it becomes easy for us to deal
 with String objects. This has got nothing to do with networking.</p>
<p>DataInputStream in = new DataInputStream(sin);
 DataOutputStream out = new DataOutputStream(sout);</p>
<p>
 The rest is easy. Because it just deals with the stream objects you created,
 and not with sockets. You can use your favorite
 stream, call your favorite methods, somehow ensure the data reaches the other
 end. Read up on streams if you are not
 comfortable.</p>
<p>I hope I enlightened you all by introducing the fabulous world of network programming.
 Feel free to shoot your questions,
 I'll answer them if I can. You can also give me your valuable feedback, suggestions,
 or the mistakes you found in this tutorial.</p>
<p><font size=4>And yes, if you found this useful, go to that Your Vote! section below and vote for me!</font>

