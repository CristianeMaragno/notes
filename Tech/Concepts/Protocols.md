A protocol is a set of rules and standards that define how information is exchanged between devices and systems.
#### Internet Protocol (IP)
IP is responsible for routing packets of data to their correct destination.

Because the Internet is a global network of computers each computer connected to the Internet must have a unique address. Internet addresses are in the form nnn.nnn.nnn.nnn where nnn must be a number from 0 - 255. This address is known as an IP address.

If you connect to the Internet through an Internet Service Provider (ISP), you are usually assigned a temporary IP address for the duration of your dial-in session. If you connect to the Internet from a local area network (LAN) your computer might have a permanent IP address or it might obtain a temporary one from a DHCP (Dynamic Host Configuration Protocol) server.

Ex:
When a packet arrives at a router, the router examines the IP address put there by the IP protocol layer on the originating computer. The router checks it's routing table. If the network containing the IP address is found, the packet is sent to that network. If the network containing the IP address is not found, then the router sends the packet on a default route, usually up the backbone hierarchy to the next router. Hopefully the next router will know where to send the packet. If it does not, again the packet is routed upwards until it reaches a NSP backbone. The routers connected to the NSP backbones hold the largest routing tables and here the packet will be routed to the correct backbone, where it will begin its journey 'downward' through smaller and smaller networks until it finds it's destination.

IP is an unreliable, connectionless protocol. 
IP doesn't care whether a packet gets to it's destination or not. 
Nor does IP know about connections and port numbers. 
IP's job is too send and route packets to other computers.

![[Captura de tela de 2023-09-28 12-34-42.png]]

Interesting commands
>ping
>traceroute

#### Transmission Control Protocol (TCP)
The messages you transmit to other computers must be transmitted over whatever kind of wire connects your computer/router to the Internet. Therefore the message must be translated from alphabetic text into electronic signals, transmitted over the Internet, then translated back into alphabetic text. 

Each stack layer that the message passes through may break the message up into smaller chunks of data known as packets. Each packet is assigned a port number. 

TCP is responsible for routing application protocols to the correct application on the destination computer. To accomplish this, port numbers are used. Ports can be thought of as seperate channels on each computer. For example, you can surf the web while reading e-mail. This is because these two applications (the web browser and the mail client) used different port numbers. When a packet arrives at a computer and makes its way up the protocol stack, the TCP layer decides which application receives the packet based on a port number.
 
The TCP header looks like this:
![[Captura de tela de 2023-09-28 12-32-31.png]]

Portas comuns:
FTP 20/21
Telnet 23
SMTP 25
HTTP 80

#### User Datagram Protocol (UDP)
The main difference between TCP (transmission control protocol) and UDP (user datagram protocol) is that TCP is a connection-based protocol and UDP is connectionless. While TCP is more reliable, it transfers data more slowly. UDP is less reliable but works more quickly. This makes each protocol suited to different types of data transfers.

UDP: Anything where you don't care too much if you get all data always
- Tunneling/VPN (lost packets are ok - the tunneled protocol takes care of it)
- Media streaming (lost frames are ok)
- Games that don't care if you get every update
- Local broadcast mechanisms (same application running on different machines "discovering" each other)

TCP: Almost anything where you have to get all transmitted data
- Web
- SSH, FTP, telnet
- SMTP, sending mail
- IMAP/POP, receiving mail

#### Domain Name System (DNS)
What if the you need to access a web server referred to as www.anothercomputer.com? How does your web browser know where on the Internet this computer lives? The answer to all these questions is the Domain Name Service or DNS. The DNS is a distributed database which keeps track of computer's names and their corresponding IP addresses on the Internet.

Many computers connected to the Internet host part of the DNS database and the software that allows others to access it. These computers are known as DNS servers. No DNS server contains the entire database; they only contain a subset of it. If a DNS server does not contain the domain name requested by another computer, the DNS server re-directs the requesting computer to another DNS server.

#### Hypertext Transfer Protocol(HTTP) and Hypertext Transfer Protocol Secure(HTTPS)
HTTP is the protocol that web browsers and web servers use to communicate with each other over the Internet. It is an application level protocol because it sits on top of the TCP layer in the protocol stack and is used by specific applications to talk to one another.

HTTP is a connectionless text based protocol. Clients (web browsers) send requests to web servers for web elements such as web pages and images. After the request is serviced by a server, the connection between client and server across the Internet is disconnected. A new connection must be made for each request. Most protocols are connection oriented. This means that the two computers communicating with each other keep the connection open over the Internet. 

Generations:
- HTTP/0.9 1991: One liner having a single method called GET
```
GET /index.html
```

- HTTP/1.0 1996:  Could now deal with other response formats i.e. images, video files, plain text or any other content type as well. It added more methods (i.e. POST and HEAD), request/response formats got changed, HTTP headers got added to both the request and responses, status codes were added to identify the response. One of the major drawbacks of HTTP/1.0 were you couldn’t have multiple requests per connection. That is, whenever a client will need something from the server, it will have to open a new TCP connection and after that single request has been fulfilled, connection will be closed. 
```
GET / HTTP/1.0
Host: cs.fyi
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: */*
```

- HTTP/1.1 1997: New HTTP methods were added, which introduced PUT, PATCH, OPTIONS, DELETE. HTTP/1.1 introduced the persistent connections i.e. connections weren’t closed by default and were kept open which allowed multiple sequential requests. Pipelining It also introduced the support for pipelining, where the client could send multiple requests to the server without waiting for the response from server on the same connection and server had to send the response in the same sequence in which requests were received.

- HTTP/2 2015: was designed for low latency(very small delay times) transport of content and is mainly used currently. The key features are
	1. Binary Protocol: Binary instead of Textual
	2. Multiplexing: Uses frames and streams for requests and responses, once a TCP connection is opened, all the streams are sent asynchronously through the same connection and in turn, the server responds in the same asynchronous way
	3. Header Compression: When we are constantly accessing the server from a same client there is alot of redundant data that we are sending in the headers over and over, so it was introduced header compression.
	4. Server Push: The server, knowing that the client is going to ask for a certain resource, can push it to the client without even client asking for it
	5. Request Prioritization: A client can assign a priority to a stream by including the prioritization information in the HEADERS
	6. Security:  TLS encryption
#### Secure Sockets Layer/Transport Layer Security (SSL/TLS)
Comic explaining
https://howhttps.works/https-ssl-tls-differences/

#### Internet Control Message Protocol (ICMP)
The Internet Control Message Protocol (ICMP) is a protocol that devices within a network use to communicate problems with data transmission. In this ICMP definition, one of the primary ways in which ICMP is used is to determine if data is getting to its destination and at the right time. This makes ICMP an important aspect of the error reporting process and testing to see how well a network is transmitting data. However, it can also be used to execute distributed denial-of-service (DDoS) attacks.

CMP is different from Internet Protocol (IP) version 6 or IPv6 in that it is not associated with Transmission Control Protocol (TCP) or User Datagram Protocol (UDP). As a result, there is no need for a device to connect with another prior to sending an ICMP message. 

For example, in TCP, the two devices that are communicating first engage in a handshake that takes several steps. After the handshake has been completed, the data can be transferred from the sender to the receiver. This information can be observed using a tool like tcpdump. 

ICMP is different. No connection is formed. The message is simply sent. Also, unlike with TCP and UDP, which dictate the ports to which information is sent, there is nothing in the ICMP message that directs it to a certain port on the device that will receive it.

#### Simple Mail Transfer Protocol (SMTP)
SMTP is also a text based protocol, but unlike HTTP, SMTP is connection oriented. SMTP is also more complicated than HTTP.
When you open your mail client to read your e-mail, this is what typically happens:

1. The mail client (Netscape Mail, Lotus Notes, Microsoft Outlook, etc.) opens a connection to it's default mail server. The mail server's IP address or domain name is typically setup when the mail client is installed.
2. The mail server will always transmit the first message to identify itself.
3. The client will send an SMTP HELO command to which the server will respond with a 250 OK message.
4. Depending on whether the client is checking mail, sending mail, etc. the appropriate SMTP commands will be sent to the server, which will respond accordingly.
5. This request/response transaction will continue until the client sends an SMTP QUIT command. The server will then say goodbye and the connection will be closed.


https://cs.fyi/guide/how-does-internet-work
https://web.stanford.edu/class/msande91si/www-spr04/readings/week1/InternetWhitepaper.htm
https://cs.fyi/guide/http-in-depth
https://howhttps.works/why-do-we-need-https/