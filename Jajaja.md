![[Pasted image 20250517162613.png]]

We have a given .pcap file.

Let’s check the contents of this file with Wireshark.

![[Pasted image 20250517162707.png]]

The packets’ protocol is TCP and TLS1.2

This already excludes some tools.

Protocol hierarchy is interesting.

![[Pasted image 20250517162905.png]]

Apparently, there are no other types of packets in the file.

The most important packet for us is the client hello packet.

In the client hello packet, the JA3 fingerprint is visible.

![[Pasted image 20250517163110.png]]

This fingerprint is unique for every tool, so we can use it to identify exactly which tool was used for the attack.

Let’s Google this fingerprint.

![[Pasted image 20250517163315.png]]

The very first link takes us to GitHub.

![[Pasted image 20250517163544.png]]

From here, we learn that the attack was carried out using Metasploit's Meterpreter.

Accordingly, the flag is - dga{metepreter}
