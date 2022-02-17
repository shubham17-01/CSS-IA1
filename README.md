# CSS-IA1
CSS IA1 for Sem 6
_____________________________________________________________
## Instructions

### Installation
Python, Npcap and Scapy are required to run Scapy(Unzip the archive, open a command prompt in that directory and run python setup.py install. on windows.

Just download the files and run the setup program. Choosing the default installation options should be safe. (In the case of Npcap, Scapy will work with 802.11 option enabled. You might want to make sure that this is ticked when installing).

After all packages are installed, open a command prompt (cmd.exe) and run Scapy by typing scapy. If you have set the PATH correctly, this will find a little batch file in your C:\Python27\Scripts directory and instruct the Python interpreter to load Scapy.

##### Note: As Scapy is run entirely on terminal, the repository contains no code files. Instead, the README file contains all necessary instructions

#### Creating a packet
To create a packet you can choose any layer(Ethernet, IP) and assign it to a variable. 
The / operator has been used as a composition operator between two layers. When doing so, the lower layer can have one or more of its defaults fields overloaded according to the upper layer. (You still can give the value you want). A string can be used as a raw layer.
#### Graphical dumps
raw(pkt) - assemble the packet  
hexdump(pkt) - have a hexadecimal dump  
ls(pkt) - have the list of fields values  
pkt.summary() - for a one-line summary  
pkt.show() - for a developed view of the packet  
pkt.show2() - same as show but on the assembled packet (checksum is calculated, for instance)  
pkt.sprintf() - fills a format string with fields values of the packet  
pkt.decode_payload_as() - changes the way the payload is decoded  
pkt.psdump() - draws a PostScript diagram with explained dissection  
pkt.pdfdump() - draws a PDF with explained dissection  
pkt.command() - return a Scapy command that can generate the packet  
#### Pcaps
Packet Capture or PCAP (also known as libpcap) is an application programming interface (API) that captures live network packet data from OSI model Layers 2-7. Network analyzers like Wireshark create .pcap files to collect and record packet data from a network. PCAP comes in a range of formats including Libpcap, WinPcap, and PCAPng. You can read packets from a pcap file and write them to a pcap file. This can be done using the rdpcap() command.
#### Generating sets of packets
Example:  
a=IP(dst="www.slashdot.org/30")  
a  
<IP  dst=Net('www.slashdot.org/30') |>  
[p for p in a]  
[<IP dst=66.35.250.148 |>, <IP dst=66.35.250.149 |>,  
 <IP dst=66.35.250.150 |>, <IP dst=66.35.250.151 |>]  
#### Sending packets
The send() function will send packets at layer 3. That is to say, it will handle routing and layer 2 for you. The sendp() function will work at layer 2. It’s up to you to choose the right interface and the right link layer protocol. send() and sendp() will also return sent packet list if return_packets=True is passed as parameter.  
Example: send(IP(dst="1.2.3.4")/ICMP())
#### Send and receive packets
The sr() function is for sending packets and receiving answers. The function returns a couple of packet and answers, and the unanswered packets. The function sr1() is a variant that only returns one packet that answered the packet (or the packet set) sent. The packets must be layer 3 packets (IP, ARP, etc.). The function srp() do the same for layer 2 packets (Ethernet, 802.3, etc.). If there is no response, a None value will be assigned instead when the timeout is reached.
#### Sniffing
We can easily capture some packets or even clone tcpdump or tshark. Either one interface or a list of interfaces to sniff on can be provided. If no interface is given, sniffing will happen on conf.iface:  

Example: sniff(filter="icmp and host 66.35.250.151", count=2)
