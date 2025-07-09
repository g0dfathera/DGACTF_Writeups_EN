![[Pasted image 20250517154247.png]]

![[Pasted image 20250517154457.png]]

The site contains a Linux CLI (Command Line Interface), and our user does not have `suid`, which means we have limited permissions.

The hint mentions services running on the server. Let's check these services using the `top` command.

![[Pasted image 20250517154730.png]]

All active services are familiar except one:

```
/opt/service/vulnservice
```

Let’s try stopping the service — `kill 980` (980 is the service’s PID).

![[Pasted image 20250517154953.png]]

We cannot stop the service, as it requires root privileges.

Let’s see what the service does using the `strings` command.

![[Pasted image 20250517155455.png]]

We got very important information using `strings`.  
First, the service listens on `localhost` at port `4444`.  
Also, it uses the `cowsay` command. Let’s listen to port 4444 using `netcat` and interact with the service.

![[Pasted image 20250517155725.png]]

The service simply runs the `cowsay` command and says whatever we provide. This may be exploitable for privilege escalation.  
Let’s try breaking out of `cowsay` and gaining access to the shell.

![[Pasted image 20250517155923.png]]

As we can see, the service has root privileges. Let’s use this service to read `flag.txt` located in the root directory.

![[Pasted image 20250517160145.png]]
