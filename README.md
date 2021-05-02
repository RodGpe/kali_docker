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
