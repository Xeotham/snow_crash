When we started the level02, in the home of the user we found the file:

```bash
----r--r-- 1 flag02 level02 8302 Aug 30  2015 level02.pcap
```
**level02.pcap** files contains TCP conversations.
We then used and installed Wireshark to visualize packets:

By turning on Analyze -> Follow -> TCP Streams, we got:
```
..%
..%
..&..... ..#..'..$
..&..... ..#..'..$
.. .....#.....'.........
.. .38400,38400....#.SodaCan:0....'..DISPLAY.SodaCan:0......xterm..
........"........!
........"..".....b........b....    B.
..............................1.......!
.."....
.."....
..!..........."
........"
..".............    ..
.....................
Linux 2.6.38-8-generic-pae (::ffff:10.1.1.2) (pts/10)

..wwwbugs login: 
l
.l
e
.e
v
.v
e
.e
l
.l
X
.X


..
Password: 
ft_wandr...NDRel.L0L

.
..
Login incorrect
wwwbugs login: 
```

To see the password correctly we turned Hex Dump: 

```
000000B9  66                                                 f
000000BA  74                                                 t
000000BB  5f                                                 _
000000BC  77                                                 w
000000BD  61                                                 a
000000BE  6e                                                 n
000000BF  64                                                 d
000000C0  72                                                 r
000000C1  7f                                                 .
000000C2  7f                                                 .
000000C3  7f                                                 .
000000C4  4e                                                 N
000000C5  44                                                 D
000000C6  52                                                 R
000000C7  65                                                 e
000000C8  6c                                                 l
000000C9  7f                                                 .
000000CA  4c                                                 L
000000CB  30                                                 0
000000CC  4c                                                 L
000000CD  0d                                                 .
```

7F is corresponding to the del caracter, we then deleted caracters before it.

We then got **"ft_waNDReL0L"** which is the password for the flag02 user.
