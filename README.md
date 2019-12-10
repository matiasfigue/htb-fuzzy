# Cartographer
Solution to Hack The Box Challenge - Fuzzy

### Problem

It's a web that exposes you a login form and you must discover the username and password to gain access.

### Solution
Brute-Force Attack using WFuzz and DirBuster. <br>
[DirBuster - file/folder automated discovery](https://github.com/xmendez/wfuzz)<br>
[WFuzz - web automated discovery](https://github.com/xmendez/wfuzz)

Told to DirBuster to find valid paths (files/folder) on http://www.docker.hackthebox.eu:31887

DirBuster catched /api/ directory and /api/action.php file. That return "Error: Parameter not set". Told to WFuzz to search valid parameters. hh is the length of characters in source code.
```bash
wfuzz --hh=24 -c  -w /usr/share/dirb/wordlists/big.txt http://docker.hackthebox.eu:31887/api/action.php?FUZZ=test
```

DirBuster detected that the parameter "reset" changes the lenght of the source code. The message returned said "Error: Account ID not found". So "reset" is the parameter. Now must search the value so
```bash
wfuzz --hh=27 -c -w /usr/share/dirb/wordlists/big.txt http://docker.hackthebox.eu:31887/api/action.php?reset=FUZZ
```
