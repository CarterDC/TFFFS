# Mon Home Server

## 1. Introduction

* **Le but de cette suite de documents est de maintenir des tutoriels à jour afin de pouvoir refaire à l'identique / améliorer le server privé, sans avoir & redécouvrir la roue à chaque fois.**

* **Prérequis :** 
    * Le hardware devrait intégrer un CPU Intel de préférence, avec QuickSync, pour bénéficier de l'accélération matérielle lors du transcodage Video.
    * On doit disposer d'un nom de domaine. Ici on utilisera vps-de-carter.org, managé via cloudflare.
    * La box / routeur doit pouvoir attribuer une IP fixe sur le réseau local (bail statique hors de la plage de DHCP), ici on utilise 192.168.1.69. Le routeur permet en l'occurence de fixer un nom d'hote pour la machine sur le réseau local, ici : ps-de-carter. 

---

## 2. Planification / Choix d’architecture

* **Objectifs :** 
Le but premier est d'avoir un serveur privé pour stocker une bibliothèque de média (Audio et Video). 
* **Solutions alternatives envisagées (et pourquoi ce choix) :** Très utile pour référence future. Pourquoi avoir choisi `mkdocs` plutôt que `sphinx`, ou l’authentification par clé SSH plutôt que par mot de passe ?
* **Architecture système / Schéma réseau (si applicable) :** Un simple diagramme (utilisable via Mermaid.js dans Material for MkDocs) peut clarifier les configurations complexes.

---

## 3. Étapes de mise en œuvre

Cette section doit être un tutoriel clair et progressif. Chaque étape contient un objectif et les commandes nécessaires.

### 3.1. [Sous-sujet 1 : par ex., Installation des paquets nécessaires]

* **Objectif :** Que cherchez-vous à accomplir à cette étape ?
* **Explication :** Pourquoi ces paquets sont-ils nécessaires ? Que font ces commandes ?
* **Commandes :** Utilisez des blocs de code avec coloration syntaxique. Précisez si des droits root sont requis.
    ```bash
    sudo apt update
    sudo apt install <nom-du-paquet> # Pourquoi ce paquet est requis
    ```
* **Sortie attendue (optionnel mais utile) :** Affichez un extrait ou un exemple de la sortie attendue pour guider le lecteur.
    ```
    Exemple de sortie...
    ```
* **Remarques / Dépannage :** Considérations spécifiques, problèmes fréquents, ou astuces utiles.

### 3.2. [Sous-sujet 2 : par ex., Configuration]

* **Objectif :** Quelle configuration mettez-vous en place ?
* **Explication :** Précisez le rôle des fichiers de configuration, les paramètres spécifiques et leurs effets.
* **Commandes (édition de fichiers) :**
    ```bash
    sudo nano /etc/config/fichier.conf
    ```
* **Contenu du fichier (utiliser un bloc code avec `linenums` et `hl_lines`) :**
    ```ini linenums="1" hl_lines="5 7-8"
    # Exemple de fichier de configuration
    [Section]
    Parametre1 = valeur1
    # Cette ligne est importante
    Parametre2 = valeur2 # Cette valeur permet de faire X
    AutreParam = 0
    # Activer ceci pour Y
    EncoreUn = true
    ```
* **Commandes de validation (ex. : `systemctl status`) :**
    ```bash
    systemctl status nom-du-service
    ```
* **Sortie attendue :**
    ```
    ● nom-du-service.service - Description
         Chargé : chargé (/lib/systemd/system/nom-du-service.service; activé; preset : activé)
         Actif : actif (en fonctionnement) depuis ...
    ```
* **Remarques / Dépannage :** Comme ci-dessus, partagez vos réflexions ou pièges courants.

---

## 4. Vérification / Tests

* **Comment vérifier que tout fonctionne :** Commandes ou étapes de test.
    ```bash
    ssh utilisateur@ip-du-serveur # Pour tester la connexion SSH
    ```
* **Résultat attendu :** Que devrait-on voir ou constater si tout fonctionne correctement ?

---

## 5. Utilisation quotidienne (si applicable)

* **Commandes courantes :** 
    ```bash
    journalctl -u sshd.service
    ```
* **Astuces :** Bonnes pratiques, raccourcis utiles, etc.

---

## 6. Maintenance / Évolutions futures

* **Mises à jour :** 
* **Problèmes potentiels :** 
* **Évolutivité / Améliorations futures :** 
    * NextCloud
    * SmartMonTools
    * Monitoring / Pilotage
    * Foundry
    * Satisfactory
    * PiHole

---

## 7. Ressources / Liens utiles

* **Articles / tutoriels pertinents :** 

---

## 8. Journal des modifications

* **Date :** Modifications apportées.
    * 20-06-2025 : Mise en place nouveau patron.

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

### virer un package : 
sudo apt purge postfix
sudo apt autoremove --dryrun pour tester s'il y ad 'autres dépendances à virer

TODO en vrac : 
script + cloudflare API pour mainteanir les A records à jour (pas d'ip fixe chez orange). ou bien ddclient.  
https://developers.cloudflare.com/dns/manage-dns-records/how-to/managing-dynamic-ip-addresses/  

