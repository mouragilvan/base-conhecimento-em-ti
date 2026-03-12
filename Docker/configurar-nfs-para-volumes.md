## Instalação do pacote do Linux
```sh
apt-get install nfs-common
```
## Verificar se NFS está rodando
```sh
sudo systemctl status nfs-kernel-server
```
## Verificar exports
```sh
sudo exportfs -v
```

## Ajustar a permissão do diretório no server de arquivos
### Opção 1
```sh
sudo chown -R 82:82 /caminho/onde/foi/criada/a-pasta/dos-arquivos
```

### Opção 2
```
sudo chmod -R 755 /caminho/onde/foi/criada/a-pasta/dos-arquivos
```

## Se não estiver configurado, adicionar:
Inserir o caminho onde os arquivos estão no seu servidor de arquivos. Os diretórios de pasta. No exemplo abaixo é /volumes/develop/servicos

```sh
echo "/volumes/develop/servicos *(rw,sync,no_subtree_check,no_root_squash)" | sudo tee -a /etc/exports
```
Ou adicionar manualmente no arquivo /etc/exports  

## Atualizar o serviço
```sh 
sudo exportfs -ra
sudo systemctl restart nfs-kernel-server
```
# Criação do volume 
## Opção 1
```sh
docker volume create -d vieux/sshfs \
  -o sshcmd=usuario@troque-pelo-ip-ou-dns:/caminho/onde/foi/criada/a-pasta/dos-arquivos \
  -o password=suasenha \
  -o port=22 \
  -o StrictHostKeyChecking=no \
  -o UserKnownHostsFile=/dev/null \
  -o allow_other \
  -o default_permissions \
  -o reconnect \
  nome_do_volume
```

## Opção 2
```sh
docker volume create -d vieux/sshfs \
  -o sshcmd=usuario@troque-pelo-ip-ou-dns:/caminho/onde/foi/criada/a-pasta/dos-arquivos \
  -o password=minhasenha \
  -o port=22 \
  -o StrictHostKeyChecking=no \
  -o UserKnownHostsFile=/dev/null \
  -o allow_other \
  -o default_permissions \
  -o uid=33 \
  -o gid=33 \
  -o reconnect \
  nome_do_volume
```

## Opção 3
```sh
docker volume create -d vieux/sshfs \
  -o sshcmd=usuario@troque-pelo-ip-ou-dns:/caminho/onde/foi/criada/a-pasta/dos-arquivos \
  -o identityfile=/root/.ssh/id_rsa \
  -o port=22 \
  -o StrictHostKeyChecking=no \
  -o UserKnownHostsFile=/dev/null \
  -o allow_other \
  -o default_permissions \
  -o reconnect \
  nome_do_volume
```

## Opção 4
```sh
docker volume create \
  --driver local \
  --opt type=nfs \
  --opt device=:/caminho/onde/foi/criada/a-pasta/dos-arquivos \
  --opt o=addr=troque-pelo-ip-ou-dns,rw,nolock \
  nome_do_volume
```
