## docker and docker compose
[install pour debian](https://docs.docker.com/engine/install/debian/)
install using the apt repo (3 étapes)

il faut s'ajouter au groupe docker
sudo usermod -aG docker $USER

### docker network 
docker network create docker_network

## foundryvtt 0.8.9
sudo adduser --system --no-create-home --group foundry_user
sudo usermod -aG vault_dwellers foundry_user


## jellyfin
sudo adduser --system --no-create-home --group jellyfin_user
sudo usermod -aG vault_dwellers jellyfin_user

