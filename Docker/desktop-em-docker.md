## Comandos para executar um desktop simples 

```sh
docker run -d \
  --name=webtop \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/Sao_Paulo \
  -p 3000:3000 \
  --shm-size=1gb \
  lscr.io/linuxserver/webtop:ubuntu-xfce
  ```