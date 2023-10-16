# Jarkom-Tugas-1-Hands-On-Wireshark

|Nama|NRP|
|----------------------------|----------|
|Laurivasya Gadhing Syahafidh|5025211136|

### **Table of Contents**
1. [TCP-Problems](#TCP-Problems)
2. [UDP-Problems](#UDP-Problems)

### **TCP-Problems**
1. What is the IP address and TCP port number used by the client computer (source) that is transferring the alice.txt file to gaia.cs.umass.edu?

``` js
Answer:
a. IP address : 192.168.86.68
b. TCP port number : 55639
```

2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?

``` js
Answer:
a. IP address : 128.119.245.12
b. Port : 80
```

3. What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? What is it in this TCP segment that identifies the segment as a SYN segment? Will the TCP receiver in this session be able to use Selective Acknowledgments?

``` 
Answer:
a. Sequence number (raw) : 4236649187
b. Look at the flags in the TCP Control Bits to identify a segment as a SYN segment
c. To determine if the TCP receiver will use Selective Acknowledgments, check the TCP options field in the initial SYN segment to see if it contains the SACK Permitted option. If it's present, then SACK is supported in that session.
```

4. What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is it in the segment that identifies the segment as a SYNACK segment? What is the value of the Acknowledgement field in the SYNACK segment? How did gaia.cs.umass.edu determine that value?

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

``` 
Answer:
a. Sequence Number (raw) : 4236649188**
b. Payload (data) size : 1448 bytes**
c. If the payload data in the TCP segment is 1448 bytes, and the file "alice.txt" is more than 152K bytes (where 1K is typically defined as 1024 bytes), then it's clear
   that the entire contents of "alice.txt" cannot fit into this single 1448-byte TCP segment.
```
6.  Consider the TCP segment containing the HTTP “POST” as the first segment in the data transfer part of the TCP connection.

* At what time was the first segment (the one containing the HTTP POST) in the data-transfer part of the TCP connection sent?
``` js
Answer: 0.147682s
```
* At what time was the ACK for this first data-containing segment received?
``` js
Answer: 0.149626s
```
* What is the RTT for this first data-containing segment?
``` 
Answer:
RTT = ACK Timestamp - Segment Sending Timestamp**
RTT = 0.149626s - 0.147682s**
RTT = 0.001944
```
* What is the RTT value the second data-carrying TCP segment and its ACK?
* What is the EstimatedRTT value (see Section 3.5.3, in the text) after the ACK for the second data-carrying segment is received?



7. What is the length (header plus payload) of each of the first four data-carrying TCP segments?

> **Answer:**

8. What is the minimum amount of available buffer space advertised to the client by gaia.cs.umass.edu among these first four data-carrying TCP segments7? Does the lack of receiver buffer space ever throttle the sender for these first four data- carrying segments?

> **Answer:**

9. Are there any retransmitted segments in the trace file? What did you check for (in the trace) in order to answer this question?

> **Answer :**

10. How much data does the receiver typically acknowledgein an ACK among the first ten data-carrying segments sent from the client to gaia.cs.umass.edu? Can you identify cases where the receiver is ACKing every other received segment (see Table 3.2 in the text)among these first ten data-carrying segments?

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

> **Answer :**

2. 3. By consulting the displayed information in Wireshark’s packet content field for this packet, determine the length (in bytes) of each of the UDP header fields.

> **Answer :**

4. The value in the Length field is the length of what?.Verify your claim with your captured UDP packet.

> **Answer :**

5. What is the maximum number of bytes that can be included in a UDP payload? (Hint: the answer to this question can be determined by your answer to 2. above)

> **Answer :**

6. What is the largest possible source port number? (Hint: see the hint in 4.)

> **Answer :**

7. What is the protocol number for UDP? Give your answer in both hexadecimal and decimal notation. To answer this question, you’ll need to look into the Protocol field of the IP datagram containing this UDP segment (see Figure 4.13 in the text, and the discussion of IP header fields).

> **Answer :**

8. Examine a pair of UDP packets in which your host sends the first UDP packet and the second UDP packet is a reply to this first UDP packet. (Hint: for a second packet to be sent in response to a first packet, the sender of the first packet should be the destination of the second packet). Describe the relationship between the port numbers in the two packets.

> **Answer :**
