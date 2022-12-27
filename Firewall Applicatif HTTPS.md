Attention il faut faire un rndc flush sur les serveurs DNS si le domaine vient d'être créée.

HTTPS Firewall Application

Se connecter sur le serveur du client ===> ip a Prendre l'ip du WAF et se connecter dessus.

Faire un `rndc flush`

`/usr/local/celeonet/bin/vhost-nginx.py artisan`

`Systemctl reload Nginx`

`systemctl reload httpd` sur le serveur du client

Vérifier le renouvellement des certificats.
