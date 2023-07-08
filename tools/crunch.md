---
description: https://www.kali.org/tools/crunch/
---

# 📁 Crunch

Crunch is a wordlist generator where you can specify a standard character set or any set of characters to be used in generating the wordlists. The wordlists are created through combination and permutation of a set of characters. You can determine the amount of characters and list size.

This program supports numbers and symbols, upper and lower case characters separately and Unicode.

\
Cheatsheet

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

