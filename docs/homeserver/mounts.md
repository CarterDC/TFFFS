On va utiliser mergerfs pour créer un point de montage virtuel et ainsi compiler tous les disques en un seul.



## Formatage
Les disques de données sont formatés en entier en ext4 (pas de partionnage nécessaire pour ce qu'on fait).

```lsblk -f``` # pour voir les file systems et uuid
```sudo mkfs.ext4 /dev/sda``` # création du file system, directement
## Montage
sudo apt install mergerfs

### Créa des répertoires
sudo mkdir drive1
sudo mkdir drive2
sudo mkdir drive3
sudo mkdir vault
sudo mkdir parity

```lsblk -f``` # pour voir les device, file systems et uuid

Montage à la main : 
sudo mount /dev/sda /mnt/disk1

Montage permanent : 
sudo nano /etc/fstab 
Rajouter 
UUID=359d90df-f17a-42f6-ab13-df13bf356de7 /mnt/disk1 ext4 defaults 0 2

Fusion des disks dans un seul dossier.  
Option à choisir, ici epmfs (existing path, most free space)

/mnt/disk1:/mnt/disk2:/mnt/disk3 /mnt/vault fuse.mergerfs defaults,allow_other,use_ino,cache.files=off,moveonenospc=true,category.create=epmfs,minfreespace=10G,default_permissions,umask=002 0 0

## Permissions
Créa d'un user system (pas de login, pas de home)
sudo useradd -r -M -s /usr/sbin/nologin samba_user
ou bien spécific debian :

sudo adduser --system --no-create-home --group samba_user

Créa d'un groupe avec tous les droits sur le vault:
sudo addgroup vault_dwellers
sudo usermod -aG vault_dwellers samba_user

(pas oublier de se rajouter soi-m^me dans le groupe : ```sudo usermod -aG vault_dwellers $(whoami)```)

ajouter vault_dwellers en proprio sur le vault (et les disques)
sudo chown -R root:media /mnt/drive1

sudo find /mnt/vault -type d -exec chmod 2775 {} \;
sudo find /mnt/vault -type f -exec chmod 664 {} \;
*à faire sur chaque drive*

Permissions ACL :  
installation de ACL :  
sudo apt install acl -y

For Samba service (full access) :  
sudo setfacl -R -m u:sambauser:rwx /mnt/vault
sudo setfacl -R -d -m u:sambauser:rwx /mnt/vault


## Parité
Le disque de parité étant neuf et non formaté on doit d'abord créer une partition. on va créer une partition sur la totalité du disque, puis formater en XFS. ext4 est limité à 16T par fichier mais XFS est plus adapté à la gestion des gros fichiers.

### Méthode interactive
sudo fdisk /dev/sdd  
puis g->n->1->enter->enter->w

### Méthode directe
sudo fdisk /dev/sdd <<EOF
g    # create a new empty GPT partition table
n    # add a new partition
[Enter]  # partition number: accept default “1”
[Enter]  # first sector: accept default (start of disk)
[Enter]  # last sector: accept default (end of disk)
w    # write table and exit
EOF

### Formatage en XFS : 
sudo apt install xfsprogs

mkfs.xfs -f -L parity /dev/sdd1

### install et config de snapraid




## note : création d'un sym link :  
sudo ln -s /mnt/vault/my_audio/music ./music_library 
sudo rm music_library pour l'enlever sans risque pour l'original
