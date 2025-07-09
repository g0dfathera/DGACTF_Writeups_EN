![[Pasted image 20250518130612.png]]

First, let's look at the hint.

![[Pasted image 20250518130653.png]]

"Knocking on heaven's door?" — maybe "Heaven's door" refers to some kind of cloud service.

Let’s scan the given IP using `nmap`.

![[Pasted image 20250518131008.png]]

Several ports are open on the IP address.

Let’s see what’s on port 80.

![[Pasted image 20250518131113.png]]

On the main page, we see Apache's default page. There might be other routes on the website. I'll use the `ffuf` tool for bruteforcing.

![[Pasted image 20250518131559.png]]

We discovered a new route — `/cloud`.

![[Pasted image 20250518131657.png]]

The index at `/cloud` contains several files. All of them are needed for `cloud.php` to function. When I saw `file.txt`, I thought the flag might be inside, but it turned out to contain a different message: "Feel the cloud."

Let’s visit `cloud.php`.

![[Pasted image 20250518131914.png]]

At first glance, the website is very simple — it displays the message from `file.txt`, uses the image found in the index as a background, and plays music from an `.mp3` file — again, "Knocking on Heaven's Door."

If we look closely at the website’s URL, we can spot a possible vulnerability — LFI (Local File Inclusion).

Let’s try a simple payload:

```
http://172.105.92.188/cloud/cloud.php?welcome=../../../../etc/passwd
```

![[Pasted image 20250518132359.png]]

Looks like the site really is vulnerable to LFI.

If we recall the `nmap` results, we saw that port 22 (SSH) is open. So I attempted to extract the `id_rsa` file (so I could log in to the server via SSH and possibly retrieve the flag), but all my attempts failed.

So I tried to read the actual `cloud.php` code using LFI to see if it contained anything interesting.

![[Pasted image 20250518132840.png]]

I didn’t see anything interesting in the browser, so I tried checking the same path with `curl`.

![[Pasted image 20250518133009.png]]

Now we’re making progress. We found a clue:

```
$hinti="you need to knock, my friend, on the port"
```

The initial hint is now clear — "knocking on heaven’s door" referred to **port knocking** on the server.

Let’s run `nmap` again, this time scanning more ports.

![[Pasted image 20250518133400.png]]

We found another port — `65124`, which is closed. To open it, you need to “knock” on other ports in a specific pattern. If you knock correctly, the port will open for a short time.

I first tried writing a bash script that would automatically knock using different patterns on the ports we already found with `nmap`: 23, 25, 22, 80. But that didn’t work — I couldn’t open the port.

Then I remembered the LFI and that the server is running Linux. On Linux systems, there’s often a config file like `knockd.conf`.

I tried to read that file’s contents — and it worked.

![[Pasted image 20250518134055.png]]

We found the ports and the timing intervals that need to be used to knock and open port 65124.

To do this, I wrote a bash script.

![[Pasted image 20250518134338.png]]

I ran the script — and it gave me the flag.

![[Pasted image 20250518134501.png]]
