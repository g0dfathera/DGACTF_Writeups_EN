We have a file in pcap format.
Let’s open it in Wireshark and see what protocols are used.

![[Pasted image 20250521142049.png]]

First, I checked the DNS packets.

![[Pasted image 20250521142255.png]]

All domains are familiar and most likely none of them will be useful to us.

Most of the packets are of SMB type. All SMB packets are encrypted.

Let’s look at the NTLMSSP packets.

![[Pasted image 20250521142616.png]]

Here we already encountered something interesting. We can use this data and the server challenge, and crack it using hashcat.

In order to decrypt the SMB packets (and get some file from SMB) we need to extract a prepared hash. For that, I will use this GitHub repo —

```
https://github.com/mlgualtieri/NTLMRawUnHide
```

![[Pasted image 20250521143803.png]]

Crack the hash using hashcat.

![[Pasted image 20250521144657.png]]

Now, since we have the password, let’s decrypt in Wireshark.

![[Pasted image 20250521145008.png]]

![[Pasted image 20250521145103.png]]

The SMB packets are now decoded. We can see SMB objects.

![[Pasted image 20250521145205.png]]

Let’s download the rar and see what’s inside.

The rar has a password, but we can still use strings to see what is stored inside.

![[Pasted image 20250521145340.png]]

The flag is inside this rar.

For bruteforcing the password, I used john.

![[Pasted image 20250521145442.png]]

![[Pasted image 20250521145700.png]]

![[Pasted image 20250521145739.png]]