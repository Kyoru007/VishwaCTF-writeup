In the task Happy Valentine's Day from cryptography category , a Portable Graphics Network  file was encrypted. And now we have to decrypt it to find their best moments pictures for the flag.
So, we were given two files at first. One is the [source.txt](https://github.com/Kyoru007/VishwaCTF-writeup/files/14473512/source.txt) which contains the code of encryption.
And the second one is [enc.txt](https://github.com/Kyoru007/VishwaCTF-writeup/files/14473515/enc.txt) which is the picture in encrypted format.

Now , from the above code we see
```
from PIL import Image
from itertools import cycle

def xor(a, b):
    return [i^j for i, j in zip(a, cycle(b))]

f = open("original.png", "rb").read()
key = [f[0], f[1], f[2], f[3], f[4], f[5], f[6], f[7]]

enc = bytearray(xor(f,key))

open('enc.txt', 'wb').write(enc)

```

the key ```key = [f[0], f[1], f[2], f[3], f[4], f[5], f[6], f[7]]``` of the encryption is the first byte of the png file , which was the image file. And that byte consists of the first 8 bits(1 byte). The header of all the PNG files are same, and since the header comes first of any png file, so we only need to put the first 8 bits of the png file in hexadecimal.
For example : ```key = [0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A]```. Now after taking the key we need to edit the code a little. As you can see from above that "original.png" was opened and encrypted using XOR. XOR is a two way method, and if you want to know the method in details I would suggest you to google it. Now all we need to do is put the encrypted file and the key in the source.txt code.
```
from PIL import Image
from itertools import cycle


def xor(a, b):
    return [i ^ j for i, j in zip(a, cycle(b))]


f = open("enc.txt", "rb").read()
key = [0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A]


enc = bytearray(xor(f, key))

open('original.png', 'wb').write(enc)
```

And after running the following code I get the flag image.


![original](https://github.com/Kyoru007/VishwaCTF-writeup/assets/114048847/51ce1094-2510-4ff3-9996-a50042ca2591)

And the flag is in the meme, and this is situation is quite familiar for hackers and ctf players Also it was kinda funny. 
So, thanks for reading my writeup and if there is any suggestions pls knock me at my discord Kyoru.#2303. 

