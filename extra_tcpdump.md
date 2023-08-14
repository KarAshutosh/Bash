# TCPDUMP 

As we said, that tcpdump has a feature to capture and save the file in a .pcap format, to do this just execute the command with -w option.

```
tcpdump -w 0001.pcap -i eth0
```

To capture packets from the destination IP, say you want to capture packets for 50.116.66.139, use the command as follows.

```
tcpdump -i eth0 dst 50.116.66.139
```

To capture packets from the source IP, say you want to capture packets for 192.168.0.2, use the command as follows.

```
tcpdump -i eth0 src 192.168.0.2
```

To read and analyze captured packet 0001.pcap file use the command with -r option, as shown below.

```
tcpdump -r 0001.pcap
```





