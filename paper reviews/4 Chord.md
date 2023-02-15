

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| Chord: A Scalable Peer-to-peer Lookup Protocol for Internet Applications |
| SIGCOMM 2001                                                 |
| CS  341                                                      |

## Summary 

-  This paper presents Chord, a game-changing solution to efficiently locate data items in peer-to-peer applications. 
- Through theoretical analysis and simulations, it has been shown to be highly efficient and scalable. 
- Chord maps key IDs to node IDs and proposes fault tolerance through failures and successor lists for lookup.

## Strengths

1. Use O(logn) memory while maintain O(logn) lookup time.
1. Decentralization: All nodes are created equal. 
1. It has good Availability and scalability.
1. They gives sound proof for the algorithm.

## Weaknesses

1. I cannot find obvious weakness as the paper addresses a well-defined problem and provides exhaustive experimental results.
2. Work remains to be done in improving Chord’s resilience against network partitions and adversarial nodes as well as its efficiency.
3. Security issues such as the potential for a malicious or buggy group of Chord participants to present an incorrect view of the Chord ring, which threatens the availability of data assuming it's cryptographically authenticated.
4. Even 1 log N messages per lookup may be too many for some applications of Chord, especially if each message must be sent to a random Internet host.

## Justification

1. The finger table enables log-N time lookups with log-N hops, as one finger takes you approximately halfway to the target. Therefore, the lookup procedure is logarithmic, with O(logn) memory usage and lookup time.
2. Chord's decentralization ensures that every node functions as a root, eliminating root hotspots. Communication costs and the state maintained by each node scale logarithmically with the number of Chord nodes.
3. The maintenance of failures and successor lists on each node ensures fault tolerance.





P2P,  下载了歌, 就可以被别人下载. 所以受欢迎的歌可以更快找到, 给别人下载.  也就是bit 种子. 退出时会告诉successor. bit种子, 是可以找很多人下载, 每个人下载一部分, 你可以更快, 别人节省了带宽. 

网速变快了, 没人用迅雷了, 没人下载了, 都在线看. 文字也没人看了. 都看视频了.

一开始微软用CAN, 内容address 网络, 但是维度太多太复杂,没人用. 
