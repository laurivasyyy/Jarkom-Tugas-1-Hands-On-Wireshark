# Jarkom-Tugas-1-Hands-On-Wireshark

|Nama|NRP|
|----------------------------|----------|
|Laurivasya Gadhing Syahafidh|5025211136|

### **Table of Contents**
1. [TCP-Problems](#TCP-Problems)
2. [UDP-Problems](#UDP-Problems)

### **TCP-Problems**
1. What is the IP address and TCP port number used by the client computer (source) that is transferring the alice.txt file to gaia.cs.umass.edu?

![no-1](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-1.png)
``` js
Answer:
a. IP address : 192.168.86.68
b. TCP port number : 55639
```

2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?

![no-2](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-2.png)

``` js
Answer:
a. IP address : 128.119.245.12
b. Port : 80
```

3. What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? What is it in this TCP segment that identifies the segment as a SYN segment? Will the TCP receiver in this session be able to use Selective Acknowledgments?

![no-3](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-3.png)
``` 
Answer:
a. Sequence number (raw) : 4236649187
b. Look at the flags in the TCP Control Bits to identify a segment as a SYN segment
c. To determine if the TCP receiver will use Selective Acknowledgments, check the TCP options field in the initial SYN segment to see if it contains the SACK Permitted option. If it's present, then SACK is supported in that session.
```

4. What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is it in the segment that identifies the segment as a SYNACK segment? What is the value of the Acknowledgement field in the SYNACK segment? How did gaia.cs.umass.edu determine that value?

![no-4](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-4.png)

``` 
Answer:
a. Sequence number (raw) : 1068969752
b. Look at the flags in the TCP Control Bits to identify a segment as a SYNACK segment
c. Acknowledge number (raw) : 4236649188
d. Here's how gaia.cs.umass.edu determined that value:
   1. The client (gaia.cs.umass.edu) initiated the TCP connection by sending a SYN segment to the server.
   2. In the client's SYN segment, it chose an initial sequence number (ISN) and included it in the Sequence Number field. Let's say the ISN is X.
   3. When the server (the destination) received the SYN segment from gaia.cs.umass.edu, it acknowledged the receipt of this segment by sending a SYN-ACK segment in response.
   4. In the SYN-ACK segment, the Acknowledgment Number field is set to X + 1. This is because the server is acknowledging the receipt of the client's SYN segment, and
      it acknowledges it by specifying the next expected sequence number (X + 1).
```
 5. What is the sequence number of the TCP segment containing the header of the HTTP POST command?. How many bytes of data are contained in the payload (data) field of this TCP segment? Did all of the data in the transferred file alice.txt fit into this single segment?

![no-5](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-5.png)
``` 
Answer:
a. Sequence Number (raw) : 4236801228
b. Payload (data) size : 1385 bytes
c. If the payload data in the TCP segment is 1385 bytes, and the file "alice.txt" is more than 152K bytes (where 1K is typically defined as 1024 bytes), then it's clear
   that the entire contents of "alice.txt" cannot fit into this single 1448-byte TCP segment.
```
6.  Consider the TCP segment containing the HTTP “POST” as the first segment in the data transfer part of the TCP connection.

![no-6a](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-6a.png)
* At what time was the first segment (the one containing the HTTP POST) in the data-transfer part of the TCP connection sent?
``` js
Answer: 0.147682s
```

![no-6b](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-6b.png)

* At what time was the ACK for this first data-containing segment received?
``` js
Answer: 0.149626s
```
* What is the RTT for this first data-containing segment?
``` 
Answer:
RTT = ACK Timestamp - Segment Sending Timestamp**
RTT = 0.149626s - 0.147682s
RTT = 0.001944
```
* What is the RTT value the second data-carrying TCP segment and its ACK?
``` 
Answer:
RTT = ACK Timestamp - Segment Sending Timestamp
RTT = 0.149629s - 0.147682s
RTT = 0.001947s
```
* What is the EstimatedRTT value (see Section 3.5.3, in the text) after the ACK for the second data-carrying segment is received?
```
Answer:
EstimatedRTT = (1 – α) • EstimatedRTT + α • SampleRTT
EstimatedRTT = (1 – 0.125) • 0.001944 + 0.125 • 0.001944
EstimatedRTT = 0.875 • 0.001944 + 0.125 • 0.001944
EstimatedRTT = 0,001701 + 0.000243
EstimatedRTT = 0,001944s
```

7. What is the length (header plus payload) of each of the first four data-carrying TCP segments?

![no-7.1](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-7.1.png)   

![no-7.2](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-7.2.png)

![no-7.3](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-7.3.png)

![no-7.4](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-7.4.png)
``` 
Answer:
Packet 1: header = 44 bytes; payload = 0 byte 
Packet 2: header = 40 bytes; payload = 0 byte 
Packet 3: header = 32 bytes; payload = 0 byte 
Packet 4: header = 32 bytes; payload = 1448 bytes 
```

8. What is the minimum amount of available buffer space advertised to the client by gaia.cs.umass.edu among these first four data-carrying TCP segments7? Does the lack of receiver buffer space ever throttle the sender for these first four data- carrying segments?
```
Answer :
Packet 1: Window = 65535
Packet 2: Window = 28960
Packet 3: Window = 2058
Packet 4: Window = 2058

Therefore the minimum amount of available buffer space advertised to 
the client by gaia.cs.umass.edu among the first four data-carrying TCP 
segments is 2058 bytes.
```

9. Are there any retransmitted segments in the trace file? What did you check for (in the trace) in order to answer this question?

![no-9](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/tcp-9.png)
``` 
Answer :
Yes, the lack of receiver buffer space can throttle the sender by 
causing it to slow down its data transmission rate to ensure that data 
is not lost or congested at the receiver's end.
```

10. How much data does the receiver typically acknowledgein an ACK 
among the first ten data-carrying segments sent from the client to gaia.
cs.umass.edu? Can you identify cases where the receiver is ACKing every 
other received segment (see Table 3.2 in the text)among these first ten 
data-carrying segments?

> **Answer :**

11. What is the throughput (bytes transferred per unit time) for the TCP connection? Explain how you calculated this value.

> **Answer :**

12. Use the Time-Sequence-Graph(Stevens) plotting tool to view the sequence number versus time plot of segments being sent from the client to the gaia.cs.umass.edu server. Consider the “fleets”of packets sent around t= 0.025, t=0.053, t=0.082 and t=0.1. Comment on whether this looks as if TCP is in itsslow start phase, congestion avoidance phase or some other phase.Figure 6 shows a slightly different view of this data.

> **Answer :**

13. These “fleets”of segments appear to have some periodicity. What can you say about the period?

> **Answer :**

14. Answer each of two questions above for the trace that you have gathered when you transferred a file from your computer to gaia.cs.umass.edu

> **Answer :**

### **UDP-Problems**
1. Select one UDP packet from your trace. From this packet, determine how many fields there are in the UDP header. Name these fields.
![no1](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/cf9368651a09e58aaed88d12b648b20c082a1721/assets/udp-1.1.png)
```
Answer :
a. Packet number   : 5 
b. SSDP
c. There are four fields : Source port, Destination port, Length, and Checksum
```

2. By consulting the displayed information in Wireshark’s packet content field for this packet, determine the length (in bytes) of each of the UDP header fields.

![no2](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-2.1.png)

![no2.1](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-2.2.png)

![no2.2](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-2.3.png)

![no2.3](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-2.4.png)

![no2.4](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-2.5.png)
```
Answer :
The UDP header has a fixed length of 8 bytes. Each of these 4 header 
fields is 2 bytes long
```

3. The value in the Length field is the length of what?.Verify your claim with your captured UDP packet.
![no3](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-4.png)
```
Answer :
The length field specifies the number of bytes in the UDP segment 
(header plus data). An explicit length value is needed since the size 
of the data field may differ from one UDP segment to the next.

The length of UDP payload for selected packet is 275 bytes. 
283 bytes - 8 bytes = 339 bytes.
```

4. What is the maximum number of bytes that can be included in a UDP payload? (Hint: the answer to this question can be determined by your answer to 2. above)
```
Answer :
The maximum number of bytes that can be included in a UDP payload is (2^16 – 1) bytes plus the header bytes. 
This gives 65535 bytes – 8 bytes = 65527 bytes. 
```

5. What is the largest possible source port number? (Hint: see the hint 
in 4.)
```
Answer :
The largest possible source port number is (2^16 – 1) = 65535. 
```

6. What is the protocol number for UDP? Give your answer in both hexadecimal and decimal notation. To answer this question, you’ll need to look into the Protocol field of the IP datagram containing this UDP segment (see Figure 4.13 in the text, and the discussion of IP header fields).

![no6](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-6.png)
```
Answer : 
The IP protocol number for UDP is 0x11 hex, which is 17 in decimal value.
```

7. Examine a pair of UDP packets in which your host sends the first UDP packet and the second UDP packet is a reply to this first UDP packet. (Hint: for a second packet to be sent in response to a first packet, the sender of the first packet should be the destination of the second packet). Describe the relationship between the port numbers in the two packets.

![no7.2](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-7.2.png)

![no7.3](https://github.com/laurivasyyy/Jarkom-Tugas-1-Hands-On-Wireshark/blob/d4ad19f6b528dbfec05a2f89213f87ad50752da3/assets/udp-7.3.png)
```
Answer : 
The source port of the UDP packet sent by the host is the same as the 
destination port of the reply packet, and conversely the destination 
port of the UDP packet sent by the host is the same as the source port 
of the reply packet.
```

