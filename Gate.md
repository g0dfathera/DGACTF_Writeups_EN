![[Pasted image 20250517143703.png]]

```
klite.dgactf.com
```

![[Pasted image 20250516193831.png]]

The very first page of the site is a Login page. First, I tried a simple SQL Injection.

![[Pasted image 20250516194445.png]]

The site turned out to be "vulnerable" to SQL Injection. After a successful login, it redirected me to the /home route. (Which, as it turned out, did not require authentication to access.)

On the new page, there was only one inscription - 

"Perhaps the threshold you have just crossed has more uses..."

If we recall the first hint, it’s easy to guess that Union Select needs to be used on the SQL database, for which I used — Sqlmap.

First, I looked at the names of the tables.

![[Pasted image 20250516200147.png]]

The scan revealed three tables – secrets; sqlite_sequence; users.

In this case, the most interesting for us is secrets. It’s time to extract information using Union Select.

![[Pasted image 20250517143531.png]]

We found the second Flag :)