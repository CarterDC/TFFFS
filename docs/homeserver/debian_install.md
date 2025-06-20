## 1. Linux Install

Debian, installé en headless, sans root user  

* Choix d'install normale (sans graphics)

* Durant l'install de Debian, on décoche les options de GUI gnome etc.. et on coche SSH Server. (moins de package = moins d'overhead = moins de surface)

* On ne rentre pas de mot de passe pour root => l'utilisateur root est déasctivé. 

* on fini avec l'install de GRUB

on peut vérifier que root est désactivé avec :  
```$ sudo grep root /etc/shadow  cut -d':' -f2```  
(TODO : rajouter explication de la commande)

Next : [SSH](ssh.md)