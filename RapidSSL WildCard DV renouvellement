Se connecter sur Digicert avec le compte NOC,
Aller dans certificates Order,rechercher lipsfrance et décocher "exact match disabled" puis cliquer sur Renew sur le certificat.

Fait avec immodvisor
	
	#Crée un certificat csr
	
	```
	cd /etc/celeonet/httpd/certificates/
	mkdir wildcard.aviseniors.com
	cd wildcard.aviseniors.com
	```
	
	#Créer un openssl.cnf
	
	copier le texte qui suit dans le répertoire /etc/celeonet/httpd/certificates/wildcard.aviseniors.com/
	
	`vim openssl.cnf`
	
	```
	[req]
	distinguished_name = req_distinguished_name
	req_extensions = v3_req
	prompt = no
	
	[req_distinguished_name]
	C = FR
	ST = FRANCE
	L = Vitry Sur Seine
	O = CELEONET
	OU = CELEONET
	CN = *.aviseniors.com
	0.emailAddress = noc@celeonet.fr

	
	[v3_req]
	keyUsage = keyEncipherment, dataEncipherment
	extendedKeyUsage = serverAuth
	#subjectAltName = @alt_names
	
	[alt_names]
	DNS.1 = aviseniors.com
	```
	
	
	#Générer une .clé csr et .key
	
	`openssl req -config openssl.cnf -new -keyout wildcard.aviseniors.com.key -out wildcard.aviseniors.com.csr -nodes`
	
	#acheter le certificat wildcard sur ssl247 
	
	-choisir un certificat positiveSSLwildcard
	
	 -bien mettre la région idf
	
	 -payer par carte bleue
	
	 -après le paiement bien mettre le csr généré dans formulaire et remplir les encadrés rouges
	
	 -prévenir Florent
	
	#Après la confirmation du client par mail il faudra crée le fichier **wildcard.aviseniors.com.crt** et **wildcard.aviseniors.com.crt-inter**
	
	dans le fichier wildcard.aviseniors.com.crt copier le **main** et le **certificat intermediaire**
