Category: [General Skills](../)

## Description ##
 
Can you crack the password to get the flag? Download the password checker here and you'll need the encrypted flag and the hash in the same directory too. Here's a dictionary with all possible passwords based on the password conventions we've seen so far.


## Thought process ##
After inspection of the provided python file level5.py, we find that MD5 is the used hashing algorithm.

The following Python code attempts to crack the password by hashing the list of potential passwords and checking if they match the provided hash value. If a match is found, it reveals the password needed to obtain the flag.

```python
import hashlib

# Read the list of passwords from "dictionary.txt"
with open("dictionary.txt", "rb") as file:
    passwords = [line.strip() for line in file]

# Read the content of the "level3.hash.bin" file
with open("level3.hash.bin", 'rb') as level5_file:
    level5_content = level5_file.read()

# Compare each password from the file with "level3.hash.bin"
for password in passwords:
    hashed_password = hashlib.md5(password).hexdigest()
    binary_content = bytes.fromhex(hashed_password)

    if binary_content == level5_content:
        print(f"Match found! Password {password.decode()} corresponds to the provided hash")
```
We run the script:
```
$ python3 pwmatcher.py 
Match found! Password 9581 corresponds to the provided hash
````
Then we run the provided python program:
```bash
$ python3 level5.py 
Please enter correct password for flag: 9581
Welcome back... your flag, user:
picoCTF{...}
```
