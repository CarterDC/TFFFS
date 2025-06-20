# Home Server

[## 1. Linux Install](debian_install.md)


[## 2. SSH](ssh.md)

[## 3. Hardening Part 1](hardening_1.md)

[## 4. Mounts](mounts.md)

[## 5. Samba](samba.md)

### Final Touches
avant le montage des disques etc... 

On a fait l'install en Fr (pas d'autre moyen pour pouvoir choisir France comme localisation).
Du coup on rajoute l'anglais dans les locales.

Dans le wizard suivant on cherche ```en_US.UTF8```
``` bash title="Bash"
sudo dpkg-reconfigure locales
```
On peut vérifier que les locales sont bonnes avec ```locale -a```  
Il faut redémarrer pour prendre en compte la nouvelle langue par défault.

TODO en vrac : 
augmenter la partition de swap de 1G à 8G ?
virer ipv6 ?