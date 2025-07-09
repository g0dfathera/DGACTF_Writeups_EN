![[Pasted image 20250517150029.png]]

We are given a `.json` file.

![[Pasted image 20250517150200.png]]

Using `grep` did not yield any entries in flag format.

Interestingly, in this JSON file, two parameters are Hex-encoded — `params1` and `params2`.

```
"params1":"646973706c6179416c6c436f6c756d6e733d38374636475a","params2":"6c6f67696e6e616d653d30"
```

It’s possible that the flag is hidden in the decoded versions of these hex values.

We can use Python for decoding.

![[Pasted image 20250517151108.png]]

The decoded value contains the flag — but only part of it...

The hint was: **1 + 1 = 2**

This suggests the flag is split into two parts and stored separately in the JSON file.

![[Pasted image 20250517151316.png]]

With a small code adjustment, we were able to retrieve both parts of the flag, and this task is now complete.
