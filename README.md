# hondasnet
Reverse engineering Honda's S-NET protocol

### Data line info
Shortest period: 100-101us
Baud rate: 10k
Voltage Range: 0-5v with negative voltage spikes on falling edge (different module sending this?)

#### How to calculate the 7 Byte Packet Checksum:
b6 = mod(sum(b0:b5),-256)*-1

### Todo:
- What modules are sending what?


### Example session sequence:

#### Init
1.  93 46 FF FF < no checksum?
2.  09 40 7A F7 < no checksum?
3.  59 07 BB 77 7A 77 7D
4.  59 07 BB 77 71 77 86 < seems to repeat until the sending module receives a response because I've seen occur 2-3x depending on the session.

#### Key exchange?
5. 95 07 2E 91 1F 85 01 < last 4 bytes always vary

#### Loop
Constant for remainder of the session
6. 59 07 BB FC C5 5E C6
7. 95 07 1A 91 1F 85 15

## Notes
95 07 2E 91 1F 85 01
95 07 1A 91 1F 85 15

| x | x |
| y | y |
|x  | x |
|--|--|
| x |x  |


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1MDUzMjAzMV19
-->