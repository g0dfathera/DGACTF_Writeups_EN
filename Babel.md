![[Pasted image 20250517143743.png]]

```
babel.dgactf.com
```

![[Pasted image 20250517143902.png]]

On the first page, we see a hint that we might need some sort of automation or bruteforcing. Let’s move to the next page.

![[Pasted image 20250517144040.png]]

Interesting — we are given a list of routes/folders, each containing a `.txt` file with the same name.

![[Pasted image 20250517144128.png]]

Each document contains text in a different language. Presumably, the flag is in one of these files. Considering the given hints, we need some automation that will extract the text from all these documents.

I wrote a Python script that extracts text from all the files and stores it in one text document.

![[Pasted image 20250517145630.png]]

In `all-flags_content.txt`, as I suspected, the flag was found.

![[Pasted image 20250517145845.png]]
