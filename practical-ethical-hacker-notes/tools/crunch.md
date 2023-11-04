---
description: https://www.kali.org/tools/crunch/
---

# 📁 Crunch

## What is Crunch?

Crunch is a wordlist generator where you can specify a standard character set or any set of characters to be used in generating the wordlists. The wordlists are created through combination and permutation of a set of characters. You can determine the amount of characters and list size.

This program supports numbers and symbols, upper and lower case characters separately and Unicode.

## Cheatsheet

```
-b: specifies the maximum size of the wordlist.
-c: specifies the number of lines to write to the wordlist.
-d: limits the number of duplicate characters
-e: stop generating words at a certain string
-f: specifies a list of character sets from the charset.lst file
-i: inverts the order of characters in the wordlist
-l: allows the literal interpretation of %,@^ when using -t
-o: specifies the output wordlist file
-p: prints permutations without repeating characters.
-q: Like the -p option but it reads the strings from a specified file
-r: resumes a previous session (cannot be used with -s)
-s: specifies a particular string to begin the wordlist with
-t: sets a specific pattern of @,%^
-z: compresses the output wordlist file, accompanied by -o
@represents lowercase letters
^represents special characters
% represents numbers
, represents uppercase letters
```

## Example of usage

### To create a word list of specific numbers. &#x20;

```bash
crunch 1 2 0123456789 > wordlist.txt
```

<div align="left">

<figure><img src="../../.gitbook/assets/Schermata del 2023-07-09 17-49-15.png" alt=""><figcaption></figcaption></figure>

</div>

This command will generate a wordlist of 110 words having the one and 2 digit numbers with all combinations of digits 0, 1, 2, 3, 4, 5, 6, 7, 8, 9. you could use alphabets&#x20;

### To generate a wordlist with a specific pattern. &#x20;

```bash
crunch 9 9 -t juve^%%%%
```

Here we have 4 characters to represent some group of characters which are as follows: &#x20;

* **,** for all uppercase letters
* **@** for all lowercase letters
* **%** for all numeric characters
* **^** for all special characters

{% file src="../../.gitbook/assets/crunch 9 9 -t juve^%%%%.webm" %}

So the above command will output all the words starting with “**juve**” and then after that a special character and then 4 digit number.&#x20;

### To generate a custom wordlist with letters, symbols and numbers.as

This Step is for Mixed with  letters, Symbols, Numbers and creating a custom wordlist Run this command on Your terminal

```bash
crunch 4 8 123abcdefgh#$% -o list.txt
```

> crunch \<min> \<max> \<charset> -o \<output in text file>
>
> * **min :** It is the minimum password length.
> * **max :** It is the maximum password length.
> * **charset:** Character se to be used.
> * **-o :** Output in a textfile. along with name of the text file.

### To generate a wordlist with a permutation of some strings or characters &#x20;

```bash
crunch 1 10 -p juve 123
```

In the case of -p, the minimum size and the maximum size values are ignored by the crunch and it displays all the possible permutations. &#x20;

<div align="left">

<figure><img src="../../.gitbook/assets/Schermata del 2023-07-09 18-44-38.png" alt=""><figcaption></figcaption></figure>

</div>

The above command will give 2 permutations of “juve 123”.

### Other References:

[https://www.hackingarticles.in/a-detailed-guide-on-crunch/](https://www.hackingarticles.in/a-detailed-guide-on-crunch/)
