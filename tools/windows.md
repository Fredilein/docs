# Windows

## SMB

### Crackmapexec

> Swiss army knife for pentesting networks

```bash
crackmapexec smb -u users.txt -p passwords.txt --shares 10.10.10.149
crackmapexec smb ip --pass-pol # to get password policy (min len, lockout?, ...)
```

### SMB Client

```bash
smbclient //ip/share  # Don't forget // at beginning
smbclient -L //ip/    # List shares
```

Mount SMB Shares:

```bash
sudo mount -t cifs //ip/share /mnt/user/
sudo mount -t cifs -o 'username=admin,password=secret' //ip/share /mnt/user/
```

Get files recursively:

```bash
smb: \> recurse ON
smb: \> prompt OFF
smb: \> mget *
```

### SMB Server

Create Server on Linux host, access from Windows.

```bash
# Linux
impacket-smbserver mysharename $(pwd) -smb2support -user fredilein -password pw
# Windows
$pass = convertto-securestring 'pw' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential('fredilein', $pass)
New-PSDrive -Name fredilein -PSProvider FileSystem -Credential $cred -Root \\myip\mysharename
```

## Others

### Sysinternals Suite

> Official Microsoft tools to do everything Windows.

* _procdump64.exe_ to dump processes

{% hint style="warning" %}
_Tip for IRL_: Creates registry entry when running
{% endhint %}

### Evil-Winrm

Get a shell with username/password. Can test for winrm with crackmapexec first.

```bash
upload <local.txt>    # Easily upload kali files to windows
```

### rpcclient

```bash
rpcclient -U 'username%password' 10.10.10.149
rpcclient -U '' ip     # Sometimes let's you connect on old windows systems
```

