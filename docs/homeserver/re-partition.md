La restoration du system avec rsnapshot peut profiter d'une partition dédiée.
On table généralement sur 10 à 30% du volume system.

On va en profiter pour augmenter aussi la partition de swap de 1Go à 8Go (vraiment pas besoin d'autant avec 32Go de ram et sans hibernation).

## Désactivation de la partition actuelle de swap
Pour éviter des ennuis de redémarrage après avoir supprimé et recréé la partition de swap, on va dans fstab pour la commenter.

Au pire, une fois dans GParted on aura accès à un terminal pour monter la partition de boot et aller éditer fstab si besoin.

## GParted Live
On ne peut pas utiliser l'OS installé pour repattionner son propre disque de boot. Donc on va utiliser un autre OS sur un clef USB. 
On burn un iso de GParted Live sur une clusb avec balena etcher ou autre.

[GNOME Partition Editor](https://gparted.org/download.php)

Sur 1To, on va réduire la partiton de boot à 700Go (716 800Mo), bouger et resize la parttion de swap à 8Go (8 192Mo), dans le reste de la partition étendue, on crée une partition ext4 pour rsnapshot. Il doit rester env 223Go soit env 30%  de la partition de boot. (Très suffisant pour timeshift) 

## System Restore
On va utiliser [Rsnapshot](https://linuxconfig.org/guide-to-rsnapshot-and-incremental-backups-on-linux) pour créer des points de restoration.

todo : ajouter la config

### restoration : 
* Dry run
sudo rsync -aAXv --delete --dry-run \
  --exclude='/proc/' \
  --exclude='/sys/' \
  --exclude='/dev/' \
  --exclude='/run/' \
  --exclude='/mnt/' \
  --exclude='/media/' \
  --exclude='/swapfile' \
  --exclude='/lost+found/' \
  --exclude='/var/log/' \
  --exclude='/timeshift' \
  /timeshift/alpha.0/localhost/ /
* Real deal


- -aAX ensures all permissions, ACLs, and extended attributes are preserved.
- -v gives you verbose output—you’ll want to watch what happens.
- --delete removes any files in / that aren’t in the snapshot (so it cleans out yesterday’s chaos).
