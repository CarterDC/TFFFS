## install de cockpit
netdata ? 
les services de cockpit ne sont pas démarrés par défaut et s'arretent tous seul. 
Le seul service qui tourne et doit être enble/disable est cockpit.socket  


### Ouverrture ports ufw
sudo ufw allow from 192.168.1.0/24 to any port 9090 proto tcp
sudo ufw allow from 10.8.0.0/24 to any port 9090 proto tcp

## nullmailer
sudo apt install nullmailer
sudo nano /etc/nullmailer/remotes
smtp.office365.com smtp --port=587 --starttls --user=thrash.panda@outlook.com --pass=your-password


## SMART  
sudo apt install smartmontools smart-notifier


sudo update-smart-drivedb  
à relancer qd il ya un nv drive.

vérif pour chaque drive s'il est compatible smart et smart est activé (+ plein d'autres infos)
sudo smartctl -i /dev/sda  
sudo smartctl -a -d nvme /dev/nvme0n1  
un peu diff pour les disques nvme

test rapide  
sudo smartctl -t short /dev/sda  
une minute d'attente avant de check avec  
sudo smartctl -l selftest /dev/sda  
