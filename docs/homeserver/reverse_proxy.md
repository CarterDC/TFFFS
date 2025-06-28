on va utiliser nginx et certbot, tous deux dans un container. 
cd tutor ici : 
https://mindsers.blog/en/post/https-using-nginx-certbot-docker/


on va vérifier que la config de l'ensemble {domain, router, firewall, ngix + certbot} fonctionne grace à un dry-run : 
```docker compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run -d vps-de-carter.org```

obligé de refaire des certificats aussi pour jellyfin
(avec le full docker configuré (nginx + certbot)) : 
docker compose run --rm certbot certonly --webroot-path /var/www/certbot -d jellyfin.vps-de-carter.org
choisir la réponse 2 : "2: Saves the necessary validation files to a .well-known/acme-challenge/ directory within the nominated webroot path. A separate HTTP server must be running and serving files from the webroot path. HTTP challenge only (wildcards not supported). (webroot)"


  on oublie pas de créer le A record pour jellyfin sur le domain provider

  ## jellyfin 

  ### Hardware Acceleration
  getent group render (le group auquel on doit ajouter jellyfin_user) on doit aussi passer ce group dans le docker compose yml
  
  ls -l /dev/dri -> affiche les devices on vérifie qu'on abien renderD128
  drivers
  sudo apt install intel-media-va-driver-non-free libva-utils

  ## certif pour navidrome
docker compose run --rm certbot certonly --webroot-path /var/www/certbot -d navidrome.vps-de-carter.org