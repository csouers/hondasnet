# hondasnet
Reverse engineering Honda's S-NET protocol

Shortest period: 100-101us
Baud rate: 10k
Voltage Range for packet A: 0-5
^^                       B: 0-5 with negative voltage spikes on falling edge (different module sending this?)

7 Byte Packet Checksum:
b6 = mod(sum(b0:b5),-256)*-1

Todo:
- What modules are sending what?

--Session sequence--

Init:
1.  93 46 FF FF < no checksum?
2.  09 40 7A F7 < no checksum?
3.  59 07 BB 77 7A 77 7D
4a. 59 07 BB 77 71 77 86 < seems to repeat until the sending module receives a response because I've seen occur 2-3x depending on the session.

Key exchange?:
5. 95 07 2E 91 1F 85 01 < last 4 bytes always vary

Loop:
6a. 59 07 BB FC C5 5E C6 < These two packets are consistent for the session
7a. 95 07 1A 91 1F 85 15 < These two packets are consistent for the session
