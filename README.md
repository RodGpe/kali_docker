# kali_docker
Manual para usar kali con docker
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
# su -s /bin/bash rodrigo
```
