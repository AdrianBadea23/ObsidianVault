
### What is a socket?
sockets = a way to speak to other programs using standard UNIX file descriptors(Everything in UNIX is a file so any sort of IO is done by reading or writing to a file descriptor).

File descriptor = integer associated with an open file.

File can be a network connection, a FIFO, a pipe, a terminal, a real on the disk file, or anything else.

#### Raw Sockets are powerful - look into it

#### Stream sockets
Stream sockets are a reliable 2 way connected communication streams. If you output 2 items into the socket in the order "1, 2" they will arrive in the order "1, 2" at the opposite end. They will also be error free.

How do sockets achieve this level of data transmission quality? They use the Transmission Control Protocol aka TCP.

#### Datagram Sockets
Datagram sockets also use IP for routing but they dont use TCP they use the User Datagram Protocol, or UDP.

Connectionless - you dont have to maintain an open connection as you do with stream sockets. Build a packet, tell the IP with the destination information and send it. Used when TCP stack is unavailable or when few dropped packets wont matter much.

### Data Encapsulation
How it works: a packet is born, the packet is wrapped(encapsulated) in a header by the first protocol, then the whole thing(header included) is encapsulated again by the next protocol(say, UDP), then again by the next(IP), then again by the final protocol on the hardware(physical) layer(Ethernet).

#### Layered Network Model:
* Application - as far from the physical layer as you can imagine
* Presentation
* Session
* Transport
* Network
* Data Link
* Physical - hardware

### IP Addresses, version 4 and 6
IPv4 - addresses made up of 4 bytes(octets) - 192.0.2.111
IPv6 - many more addresses - 2001:0db8:c9d2:aee5:73e3:934a:a5ae:9551

#### Subnets
With IPv4 you might have 192.0.2.12, the first three bytes are the network address and the last byte was the host, or we are talking about host 12 on the 129.0.2.0 address.

The network portion of your IP address is called the netmask, which you bitwise AND with the IP address and get the network number out of it. A netmask looks something like this 255.255.255.0.

You may have a netmask like this: 255.255.255.252 which has 30 bits of network and 2 bits of host allowing for 4 hosts on the network. The new style is something like this IP/Network_bits aka
192.0.2.12/30. For IPv6 you have something like this: 2001:db8::/32 or 2001:db8:5413:4028::9db9/64.

#### Port Numbers
Besides an IP address that is used by TCP and UPD, there is another address that needs to be used, the port number. The port number is a 16 bit number thats like the local address for the connection. Ports under 1024 are considered special and usually require special OS privileges to use.

#### Byte Order
If you want to represent  the two-byte hex number b34f you will store it into sequential bytes b3 followed by 4f. This is Big-Endian(Network Byte Order).

Anything with an Intel processor sore the bytes reversed, so b34f would be stored 4f followed by b3. This is Little-Endian.

When building packets and fulling data structures you need to make sure your two and four-byte numbers are in Network Byte Order. And you do this by always assuming that the Host Byte Order is wrong so you always run the value through a function to set it to Network Byte Order.

There are 2 types of numbers that you can convert short(2 bytes) and long(4 bytes).
![[Pasted image 20241012140352.png]]

### Structs
