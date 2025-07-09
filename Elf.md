![[Pasted image 20250517151739.png]]

We are given a file without an extension.

```
0b7133f8221d6e70cbec445196b7cf5d5ac5bc55518ac896_sick
```

First, let’s identify the file type — for that, I’ll use the `file` command in Linux.

![[Pasted image 20250517152045.png]]

Judging by the task name and objective, this file should be of ELF (Executable and Linkable Format) type — but that’s not the case.

Just in case, let’s inspect it using `strings`.

![[Pasted image 20250517152313.png]]

`strings` shows that the flag is encoded, so after running the file, it should display the decoded flag.

Let’s revisit the file header — typically, the first few bytes indicate whether a file is ELF.

```
7f 45 4c 46    -->    .ELF
```

This is exactly how the hex should begin.

![[Pasted image 20250517152808.png]]

As you can see, the first bytes are blank. So, we’ll need to manually write them in.

![[Pasted image 20250517153103.png]]

Good — it looks like we fixed one problem. To help you understand what’s going on better, here’s a quick explanation of how ELF works in general:

```
Offset  Bytes          Description
0x00    7f 45 4c 46    Magic Number: \x7fELF
0x04    02             Class: 64-bit (01 = 32-bit, 02 = 64-bit)
0x05    01             Data: Little Endian (01 = LE, 02 = BE)
0x06    01             Version: 1
0x07    00             OS ABI: System V
0x08    00             ABI Version
0x09    00...          Padding
```

That’s how the first 16 bytes of an ELF file look — defining file properties.

In our case, we fixed the header (Magic Number), but the class and endianness bytes were incorrect.

To restore the file properly, we rewrite the full 16-byte header.

![[Pasted image 20250517153702.png]]

The file is now fully restored! We just need to make it executable and run it.

![[Pasted image 20250517153805.png]]
