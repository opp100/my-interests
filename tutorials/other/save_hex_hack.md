#Save File Hex Hack
###Single Code Format:

```
ABYYYYYY XXXXXXXX

A = Byte Value
0 = 1 Byte (Only Writes 000000XX)
1 = 2 Bytes (Only Writes 0000XXXX)
2 = 4 Bytes
B = Offset Type
0 = Normal
8 = Offset from Pointer
Y = Address
X = Bytes to Write

Example:

10001FEC 00007FFF

10001FEC 00007FFF - Writes 2 Bytes Worth
10001FEC 00007FFF - Normal Offset
10001FEC 00007FFF - Writes to this Address
10001FEC 00007FFF - Writes these Bytes


Example 2:

200000E8 3B9AC9FF

200000E8 3B9AC9FF - Writes 4 Bytes Worth
200000E8 3B9AC9FF - Normal Offset
200000E8 3B9AC9FF - Writes to this Address
200000E8 3B9AC9FF - Writes these Bytes
```

###Multi Code Format:

```
4BYYYYYY XXXXXXXX
4CCCDDDD EEEEEEEE

B = Byte Value & Offset Type
0 = 1 Byte (Only Writes 000000XX)
1 = 2 Bytes (Only Writes 0000XXXX)
2 = 4 Bytes
8 = Offset from Pointer; 1 Byte (Only Writes 000000XX)
9 = Offset from Pointer; 2 Bytes (Only Writes 0000XXXX)
A = Offset from Pointer; 4 Bytes
Y = Address
X = Bytes to Write
C = Amount of times to Write
D = Increases Address by
E = Increases Value by

Example:

41004500 00000100
4004000C 00000002
​
41004500 00000100 - Writes 2 Bytes Worth
4004000C 00000002 - Writes Four Times

41004500 00000100 - Writes to this Address
4004000C 00000002 - Distance Between Writes

41004500 00000100 - Writes these Bytes
4004000C 00000002 - Increases By 2 Per Write
```

###Copy Bytes Code Format:

```
5BYYYYYY ZZZZZZZZ
5BXXXXXX 00000000

B = Offset Type
0 = Normal
8 = Offset from Pointer
Y = Address to Copy Bytes From
Z = Amount of Bytes to Copy
1 = 1 Bytes
2 = 2 Bytes
So on...
X = Address to Paste Bytes

Example:

500000A2 00000004
500000B4 00000000
500000A2 00000004 - Normal Offset
500000B4 00000000 - Normal Offset

500000A2 00000004 - Copies the Bytes from this Address
500000B4 00000000 - Pastes Bytes to this Address

500000A2 00000004 - Copies Four Bytes Worth
500000B4 00000000
```

###Value Search Code & Pointer Format:

```
8FFFGGGG HHHHHHHH
_Other Code Here, see Examples_

F = Amount of Times to Find until Writes
G = Amount of Bytes to Match
0 = 0 Byte
1 = 1 Bytes
2 = 2 Bytes
3 = 3 Bytes
and so on...
H = Search Value (GOES FROM LEFT TO RIGHT, Does Not Flip the Values)
NOTE: Can be extended in the code, See Example 2.

Example:

80030002 FFFF0000 - Search Code
18000000 00007FFF - Single Code

80030002 FFFF0000 - Searches for FFFF Three Times Until Writes
18000000 00007FFF - Must be 8 to use the Pointer from the Search Code

80030002 FFFF0000 - Requires 2 Bytes Worth to Match (In this case, FFFF0000)
18000000 00007FFF - After the Searched Value is Found, Offset this much then Writes (In this case, it doesn't Offset at all)

80030002 FFFF0000 - Searched Value
18000000 00007FFF - Replaces FFFF with 7FFF

Example 2:

80040006 FFFF0000 - Search Code
FFFF0000 00000000 - Search Code Extended
4A000000 7F7F7F7F - Multi Code
40020008 00000000 - Multi Code

80040006 FFFF0000 - Searches for FFFF0000FFFF Four Times Until Writes
FFFF0000 00000000
4A000000 7F7F7F7F - Uses Pointer from Search Code and Writes Four Bytes Worth
40020008 00000000 - Writes Twice

80040006 FFFF0000 - Requires 6 Bytes Worth to Match (In this case, FFFF0000 FFFF0000 00000000)
FFFF0000 00000000
4A000000 7F7F7F7F - After the Searched Value is Found, Offset this much then Writes
40020008 00000000 - Distance Between Writes
(Refer to the Multi Code Format spoiler for the rest of the grayed out areas)
```

###Fill Code Format:

```
ABXXXXXX YYYYYYYY
ZZZZZZZZ ZZZZZZZZ

B = Offset Type
0 = Normal
8 = Offset from Pointer
X = Writes to this Address
Y= Amount of Bytes to Write
Z = Bytes to Write (GOES FROM LEFT TO RIGHT, Does Not Flip the Values)
NOTE: Can be extended in the code, See Example.

Example:

A0004510 0000000F
11223344 55667788
99AABBCC DDEEFF00

A0004510 0000000F - Writes to this Address
11223344 55667788
99AABBCC DDEEFF00

A0004510 0000000F - Writes this many Bytes
11223344 55667788 - Bytes to Write (1)
99AABBCC DDEEFF00 - Bytes to Write (2)
```

[Reference](http://www.nextgenupdate.com/forums/ps4-game-save-modding/957405-save-wizard-custom-quick-code-formats.html)
