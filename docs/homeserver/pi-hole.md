installation de pi-hole nativement (pas dans un container). On pourrait utiliser un container avec le network en mode host. Sinon, le bridge interne de docker risque de masquer des infos pertinentes sur les clients. 

l'install en elle meme consiste en l'execution d'un script depuis le site de pi-hole.net.

On peut le DL et l'exécuter dans la foulée avec un pipe vers bash  
curl -sSL https://install.pi-hole.net | bash

durant l'install, on confirme que le server a bien une ip fixe, on choisi l'inteface sur laquelle pi-hole doit communiquer eth0, enop0s3 ou eno1 suivant les sysèmes. bcp d'autres interfaces apparaissent si dockeer est déjà configuré, notament le bridge (br) et des interfaces vituelles (veth).  

On choisi à la fin le service DNS qui résoud les requetes une fois qu'elles ont été filtrées. Cloudflare est une bonne option mais on peut vouloir garder les DNS orange pour plus de facilité avec le boitier TV.  

A la fin de l'installation on peut noter le mdp, mais on va le changer de toute façon avec sudo pihole setpassword (pas besoind e l'ancien mdp)  

On règle ensuite le conflit de ports avec notre proxy déjà en écoute sur les ports 80 et 443.
sudo nano /etc/pihole/pihole.toml  
// on cherche la ligne
port = "80o,443os,[::]:80o,[::]:443os"
// on remplace par 
port = "8080o,8443os,[::]:8080o,[::]:8443os"

et on redémarre pi-hole avec la nouvelle config 
sudo systemctl restart pihole-FTL

### Firewall
il faut de toute évidence ouvrir le port 53 pour les requetes DNS :  
sudo ufw allow 53/tcp comment 'Allow DNS (TCP) for query resolution'
sudo ufw allow 53/udp comment 'Allow DNS (UDP) for query resolution'

Comme avec la livebox on doit aussi remplacer le DHCP (sinon on ne peut pas imposer notre dns) :  
sudo ufw allow 67/udp comment 'Allow DHCP (UDP) for client IP assignment'


enfin on authorise l'access local aux nouveaux ports de l'interface web de pihole :  
sudo ufw allow from 192.168.1.0/24 to any port 8080 proto tcp comment 'Allow Pi-hole Admin Web UI from LAN'
sudo ufw allow from 192.168.1.0/24 to any port 8443 proto tcp comment 'Allow Pi-hole Admin Web UI from LAN'

## config interface server
pour que pi-hole puisse filter les queries sortant du server et surtout les logger (indispensable pour un bon monitoring)

``` bash title="Bash"
sudo nano /etc/network/interfaces
```
``` bash title="interfaces"
# modifier dns-nameservers vers localhost et la gateway en secondary (optionnel)
iface enp0s31f6 inet static
    address 192.168.1.69
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 127.0.0.1 192.168.1.1
```
 sudo systemctl restart networking

## Config Livebox
suffit de décocher le service DHCP  
virer ipv6 peut aider il parait  


### tuto pour le boitier TV

https://forums.framboise314.fr/viewtopic.php?t=5960
https://www.journaldufreenaute.fr/configurer-pi-hole-utiliser-dns-dorange/

## config pihole 
Local DNS : 
ps-de-carter.home (pour continuer de se co en ssh avec carter@ps-de-carter)  
ajouter la résolution des services locaux (navidrome, jellyfin, foudry etc.. )
### DNS Hairpinning Avoidance
On va éviter que les requetes qu'on fait vers jellyfin.vps-de-carter.org partent se faire résoudre à l'extérieur pour revenir ensuite au m^me réseau local. 