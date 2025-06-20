But sécuriser l'accès en ssh.  

on peut créer une paire de clés publiques/privées

On se co en ssh avec password avec le compte créé durant l'install
``` ps1 title="Powershell"
ssh carter@ps-de-carter
```

## Private / Public Keys

### Préparation côté linux
Créa du dossier à l'emplacement classique (dans le dossier utilisateur, là où ssh va chercher les clefs)
``` bash title="Bash"
mkdir -p ~/.ssh
touch ~/.ssh/authorized_keys
```
Gestion des permissions. /!\ le dossier ET le fichiers doivent appartenir à l'utilisateur
``` bash title="Bash"
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```
A la fin, on doit obtenir ça : 
![ssh01](../assets/ssh_01.png)

### Créa des clefs sous windows
openSSH est déjà installé sur windows 11, on peut donc l'utiliser pour générer les paires de clefs.
``` ps1 title="Powershell"
ssh-keygen -t ed25519 -C "sp9-de-carter"
```
On enregistre sur place (.ssh) à coté du fichier host, sans passphrase.
On se retrouve avec 2 fichiers id_ed25519 et id_ed25519.pub (la clef publique)

Si on veut des clefs sur une autre machine, ne pas oublier de changer le label.

### Copie des clefs dans authorized_keys

copie directe depuis windows, ```>>``` concatène donc pas de soucis pour rajouter des clefs supplémentaries avec la même commande.

``` ps1 title="Powershell"
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh carter@ps-de-carter "cat >> .ssh/authorized_keys"
```

*On peut sinon, ouvrir le fichier .pub, copier le contenu et le coller dans la fentre de terminal après avoir ouvert authorized_keys avec nano.*

### Activation et Test
Pour pouvoir se co avec des clefs publiques uniquement il faut editer le fichier de config du server ssh.

``` bash title="Bash"
sudo nano /etc/ssh/sshd_config
```

On va activer les lignes suivantes (en enlevant le ```#``` de commentaire)

``` bash title="sshd_config"
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

On redémarre le service
``` bash title="Bash"
sudo systemctl restart ssh
```

Si on peut se co sans mettre de password avec juste ```ssh carter@ps-de-carter``` alors l'authentification par clefs fonctionne et on peut passer à la suite.

## IP Fixe
Si le server est bien en ip fixe, on peut restreindre ssh a cette seule interface.

Mais, l'obtention d'une IP fixe par le router n'est pas suffisante (peut arriver trop tard).
Donc on modifie les interfaces pour passer en static.
``` bash title="Bash"
sudo nano /etc/network/interfaces
```
``` bash title="interfaces"
# après 'allow-hotplug enp0s31f6'
# remplacer 'iface enp0s31f6 inet dhcp' par
iface enp0s31f6 inet static
    address 192.168.1.69
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 1.1.1.1 8.8.8.8
```
**Attention aux valeurs réelles des interfaces et IPs !**

## Config

On peut continuer l'édition de ```sshd_config```.  
Maintenant qu'on sait que les clefs fonctionnent, on va virer la co par password.

``` bash title="sshd_config"
PasswordAuthentication no
PermitRootLogin no
KbdInteractiveAuthentication no # anciennement ChallengeResponseAuthentication
UsePAM no
# le server est en ip fixe et on ne veut pas qu'il écoute sur une autre interface
ListenAddress 192.168.1.69
# On pourrait vouloir rajouter une interface pour les accès via wireguard
# ListenAddress 10.qqchose
# attention au changement de num de port !
Port 2357
```

On restart et on teste, il faut mainteantn préciser le num de port pour se co.
``` ps1 title="Powershell"
ssh -p 2357 carter@ps-de-carter
```

Next : [Hardening part 1](hardening_1.md)
