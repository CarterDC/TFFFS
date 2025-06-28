## Uncomplicated FireWall
Ufw est un front-end de iptables.
Par défault on vire tout ce qui entre.
Pour ne pas se tirer une balle dans le pied, on ajoute des accès au service ssh sur le port qu'on a défini plus tôt.

``` bash title="Bash"
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow from 192.168.1.0/24 to any port 2357 proto tcp
sudo ufw allow from 10.8.0.0/24 to any port 2357 proto tcp  # WireGuard subnet
```
*On anticipe la suite où on voudra accéder aussi via un tunnel wireguard (avec un masque de sous-réseau en 10.8.0.0/24)*

On lance le firewall.  
Cette commande active aussi ufw comme le ferait un ```systemctl enable```
``` bash title="Bash"
sudo ufw enable
```


A tout moment on peut revoir les règles ajoutées :
``` bash title="Bash"
sudo ufw status verbose # pour voir aussi les policies
sudo ufw status numbered # les numero des règles facilitent leur suppression
```


## Fail2Ban
sudo apt install fail2ban  
//on copie la conf par défaut pour éviter de se faire écraser par une update. (recommandation dans le fichier)
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local


## Monitoring