# Foundry VTT


https://foundryvtt.wiki/en/setup/hosting/Docker


## Download

Dans la section Purchased Licences du compte sur Foundry (ex: https://foundryvtt.com/community/carterdc/licenses)
Choisir node.js en OS et la version stable souhaitée, ici 0.8.9 (build 102)

Copier l'URL temporaire vers ce build (bouton TIMED URL)  
et exécuter la commande suivante pour download l'archive dans le dossier docker/foundry

 sudo wget -O foundry.zip "https://r2.foundryvtt.com/releases/8.102/FoundryVTT-8
.102.zip?verify=1750662221-RLzFoMdIXFG5nExo0rT1Aitc4Bbj1t5ciXWM9tOMYRg%3D"

Ensuite décompresser l'archive dans ./pkg avec unzip (```sudo apt install unzip``` si besoin) : sudo unzip foundry.zip -d ./pkg


update la conf nginx pour foundry pour rajouter le support des websockets :  
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
