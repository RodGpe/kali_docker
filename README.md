# kali_docker
Manual para usar kali con docker
```console
~$ docker run -it --cap-add NET_ADMIN  --privileged --net=host --env="DISPLAY" --volume="$XAUTHORITY:/root/.Xauthority:rw" -v $(pwd):/home kalilinux/kali-rolling
```
