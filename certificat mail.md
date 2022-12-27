## Modifier les chemins binaire du certificat SSL

#### Dans /etc/celeonet/dovecot/conf.d/10-ssl.conf /!\ bien commenter la dernière ligne

```
ssl_cert = </etc/ssl/celeonet/httpd/waf/comimpact.net/comimpact.net.crt
ssl_key = </etc/ssl/celeonet/httpd/waf/comimpact.net/comimpact.net.key
#ssl_ca = </etc/celeonet/ssl/mail/chain.pem
```

#### Dans /etc/postfix/main.cf /!\ ATTENTION IL Y A BIEN 4 LIGNES DIFFERENTE (smtp et smtpd)

```
smtp_tls_key_file = /etc/celeonet/httpd/certificates/toto.fr/toto.fr.key
smtp_tls_cert_file = /etc/celeonet/httpd/certificates/toto.fr/toto.fr.crt
smtpd_tls_key_file = /etc/celeonet/httpd/certificates/toto.fr/toto.fr.key
smtpd_tls_cert_file = /etc/celeonet/httpd/certificates/toto.fr/toto.fr.crt                                               ```
```



## Ajout de la tâche cron postfix

`vim /var/spool/cron/root`

```
0 12 * * * /usr/bin/systemctl restart dovecot postfix-mysql <<< copier cette ligne
```

## restart les service après le paramétrage


```
systemctl restart postfix-mysql.service dovecot.service << on restart le service
```


## Script de debug Centos 7

**pour finir copier les commandes suivante directement en ligne de commande sur le serveur**

(documentation sur https://dev.celeo.fr/wiki/dedie/install_centos7)


```
# Postfix
sed -i /'smtp_tls_CApath.*'/a'smtp_tls_exclude_ciphers = aNULL, eNULL' /etc/postfix/main.cf
sed -i /'smtpd_tls_security_level.*'/a'smtpd_tls_exclude_ciphers = aNULL, eNULL\ntls_preempt_cipherlist = yes\n\nsmtpd_tls_mandatory_ciphers = high\nsmtpd_tls_ciphers = medium\nsmtp_tls_mandatory_ciphers = high\nsmtp_tls_ciphers = medium\n\nsmtp_tls_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1, TLSv1.2\nsmtpd_tls_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1, TLSv1.2\nsmtpd_tls_mandatory_protocols = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1, TLSv1.2\nsmtp_tls_mandatory_protocols  = !SSLv2, !SSLv3, !TLSv1, !TLSv1.1, TLSv1.2' /etc/postfix/main.cf
# Dovecot
openssl dhparam -out /etc/ssl/celeonet/mail/dh.pem 2048 && sed -i /'ssl_cert'/i'ssl_min_protocol = TLSv1.2\nssl_prefer_server_ciphers = yes\n\nssl_dh=</etc/ssl/celeonet/mail/dh.pem' /etc/celeonet/dovecot/conf.d/10-ssl.conf
```