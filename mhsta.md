We are given an mp4 file.

There is nothing interesting in the video.

![[Pasted image 20250529142651.png]]

Let’s see what is hidden inside the file using strings.

![[Pasted image 20250529142739.png]]

Strings showed that powershell commands are hidden inside the file.

Let’s extract these commands.

![[Pasted image 20250529142930.png]]

Several scripts came out, I decrypted all of them and found this.

![[Pasted image 20250529144032.png]]

A new link is given, let’s check this link with curl.

![[Pasted image 20250529144200.png]]

Here is another encrypted script.

Let’s decode this one too.

![[Pasted image 20250529144616.png]]

After reverse engineering, I got this code.

![[Pasted image 20250529153024.png]]

After running it, I got the flag.

![[Pasted image 20250529153129.png]]

All dgactf challenges are solved!