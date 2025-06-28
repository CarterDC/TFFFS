sudo apt install samba
copie de la config d'origine
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak

Par défault, Samba utilise ses propres passwords ( pas lié aux passwords système)
sudo smbpasswd -a samba_user


sudo systemctl enable --now smbd

on peut tester samba en local en installant smbclient
puis
smbclient -L localhost -U samba_user

règles firewall pour le lan :
TODO : à vérifer !
peut être virer les ports supplémentaires, vu qu'on a pas besoin de la découverte et qu'on utilse pas de vieux systemes. 
- TCP 445 → Direct SMB protocol
- UDP 137, 138 → NetBIOS name resolution & discovery 
- TCP 139 → NetBIOS session service (legacy)

sudo ufw allow from 192.168.1.0/24 to any port 445 proto tcp
sudo ufw allow from 192.168.1.0/24 to any port 139 proto tcp
sudo ufw allow from 192.168.1.0/24 to any port 137,138 proto udp