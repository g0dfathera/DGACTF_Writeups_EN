I opened the previously found `.pcap` file with Wireshark and checked the Protocol Hierarchy.

![[Pasted image 20250518163603.png]]

As it turns out, most of the packets are of the DNS (Domain Name System) type.

Let’s filter the packets to show only DNS types.

![[Pasted image 20250518163739.png]]

If we observe the domains, we’ll see that only one domain is valid and familiar to us — `office365.com`.

The rest of the domains follow this pattern:

```
(hex_string).dgactf.com
```

I extracted all the hex strings and converted them into a single binary file, which I then analyzed using various tools.

To extract them, I used `tshark` (Wireshark’s CLI version):

```
tshark -r 1d5015ed19a962bda9bec653e2d72e243ccc30658dd8d4e0_crosstalk.pcap -Y "dns.qry.name" -T fields -e dns.qry.name | uniq
```

From the results, I removed any domain that didn’t contain a hex string and saved them to `domains.txt`.

Since all the hex strings in `domains.txt` had `dgactf.com` appended, I filtered out the hex parts and removed the domain suffix after the dot:

```
awk -F '.' '{print $1}' domains.txt > clean_domains.txt
```

Next, to convert the hex values into a binary file, I wrote a script in Python:

![[Pasted image 20250518164953.png]]

I then analyzed `output.bin` using `binwalk`.

![[Pasted image 20250518165057.png]]

As it turns out, the file is of `.zip` type.

Let’s save the `.bin` file as `.zip`.

![[Pasted image 20250518165145.png]]

Now extract the zip archive.

![[Pasted image 20250518165301.png]]

A PDF file was extracted.

![[Pasted image 20250518165351.png]]
