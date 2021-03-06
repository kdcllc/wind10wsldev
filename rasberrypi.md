# Raspberry Pi and DotNetCore Development

## Running `DotNetApp`

```bash
    chmod 755 ./MyWebApp
    ./MyWebApp
```

## Filesharing between Windows 10 and Raspberry  Pi

One way to make sure that the files are shared between machines is to have `Samba` installed on Raspberry Pi.
This is helpful in order to copy `AspNetCore` web applications. 

### Install and Configure `Samba`

1. Install `Samba` server.

```bash
   sudo apt update
   sudo apt-get install samba
```

2. Create shared folder

```bash
   mkdir /home/pi/shared
   chmod 777 /home/pi/shared
```

3. Configure `Samba`

- open the configuraion file

```bash
    sudo nano /etc/samba/smb.conf
```

- Enable WINS Server by modifying the following. Change `WORKGROUP` to your workgroup name.

```text
    workgroup = WORKGROUP 
    wins support = yes
```

- Adding share information

```text
[pishare]
 	comment = Pi Shared Folder
 	path = /home/pi/shared
	browsable = yes
	guest ok = yes
	writable = yes
```

(note: I was able to access this folder by going to `\\{ipaddress}\pishare`)

## Python SimpleHTTPServer: a quick way to serve a directory

```bash 
    python -m SimpleHTTPServer 8080

    python3 -m http.server 8080
```

## copy files

```bash
    scp /path/to/file username@a:/path/to/destination
```

## Check External IP address

```bash
    wget http://ipinfo.io/ip -qO -
```

```
sudo systemctl unmask hostapd
sudo systemctl enable hostapd
sudo systemctl start hostapd
```

## Revoke and remove users profiles

1. Revoke `pivpn revoke [name]`

2. Remove from the list
```bash
    # enter root
    sudo -s
    cd /etc/openvpn/easy-rsa/pki
    nano index.txt
    
    # exit root
    exit
```

Then remove all of the profiles that not needed any longer.

3. Check `pivpn list`