## instalação do pacote do Linux
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

## Se não estiver configurado, adicionar:
<p>
  Inserir o caminho onde os arquivos estão no seu servidor de arquivos. Os diretórios de pasta. No exemplo abaixo é /volumes/develop/servicos
</p>

```sh
echo "/volumes/develop/servicos *(rw,sync,no_subtree_check,no_root_squash)" | sudo tee -a /etc/exports
```
<p>
Ou adicionar manualmente no arquivo``` /etc/exports  
</p>
