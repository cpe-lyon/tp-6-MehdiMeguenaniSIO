# Exercice 1. Adressage IP (rappels)

Nous avons besoins d'utiliser 254 Machines sur un réseaau qui est 172.16.0.0/23 on veut 7 sous réseau 

172.16.0.0/23

11111111.11111111.11111110.00000000

On as besoin de 3 bits pour avoir 7 sous réseau 

Le sous réseau est donc 172.16.0.0/26

1er sous Réseau : 172.16.0.0/26

2eme sous réseau : 172.16.1.0/26

3eme Sous Reseau : 172.16.1.128/26

4eme Sous Reseau : 172.16.1.192/26

5eme Sous Reseau : 172.16..0.192/26

6eme Sous Reseau : 172.16.0.64/26

7eme Sous Reseau : 172.16.1.64/26 

# Exercice 2. Préparation de l’environnement

2. Démarrez le serveur et vérifiez que les interfaces réseau sont bien présentes. A quoi correspond l’interface
appelée lo ?

L'interface lo correspond a l'adresse boucle 

3.  Dans les versions récentes, Ubuntu installe d’office le paquet cloud-init lors de la configuration
du système. Ce paquet permet la configuration et le déploiement de machines dans le cloud via un
script au démarrage. Nous ne nous en servirons pas et sa présence interfère avec certains services (en
particulier le changement de nom d’hôte) ; par ailleurs, vos machines démarreront plus rapidement.
Désinstallez complètement ce paquet (il faudra penser à le faire également sur le client
ensuite.)

Afin d'effacer ce paquet il faut faire la commande ``` sudo apt-get purge cloud-init ```

4. Les deux machines serveur et client se trouveront sur le domaine tpadmin.local. A l’aide de la
commande hostnamectl renommez le serveur (le changement doit persister après redémarrage,
donc cherchez les bonnes options dans le manuel !). On peut afficher le nom et le domaine d’une
machine avec les commandes hostname et/ou dnsdomainname ou en affichant le contenu du fichier
/etc/hostname

Afin de modifier le hostname des Vm il faut effectuer la commande ``` hostnamectl set-hostname tpadmin.local ``` ce qui va modifier le fichier /etc/hostname

# Exercice 3. Installation du serveur DHCP

1. Sur le serveur, installez le paquet isc-dhcp-server. La commande systemctl status isc-dhcp-server
devrait vous indiquer que le serveur n’a pas réussi à démarrer, ce qui est normal puisqu’il n’est pas
encore configuré (en particulier, il n’a pas encore d’adresses IP à distribuer).

Pour installer le paquet il faut effectuer la commande ``` sudo apt-get install isc-dhcp-server ```

2. Un serveur DHCP a besoin d’une IP statique. Attribuez de manière permanente l’adresse IP 192.168.100.1
à l’interface réseau du réseau interne. Vérifiez que la configuration est correcte

Pour configurer l'adresse IP 192.168.100.1 a l'interface du réseau interne il faut modifier le netplan. 

Photo

Puis effectuer les commandes suivante ``` sudo netplan try ; sudo netplan apply ```

Puis activer l'interface ``` sudo ip link set enp0s8 up ```

3. La configuration du serveur DHCP se fait via le fichier /etc/dhcp/dhcpd.conf. Faites une sauvegarde
du fichier existant sous le nom dhcpd.conf.bak puis éditez le fichier dhcpd.conf avec les informations
suivantes :

Photo

4. Editez le fichier /etc/default/isc-dhcp-server afin de spécifier l’interface sur laquelle le serveur
doit écouter

Photo

5. Validez votre fichier de configuration avec la commande dhcpd -t puis redémarrez le serveur DHCP
(avec la commande systemctl restart isc-dhcp-server) et vérifiez qu’il est actif.

Photo

6. Notre serveur DHCP est configuré ! Passons désormais au client. Si vous avez suivi le sujet du TP 1,
le client a été créé en clonant la machine virtuelle du serveur. Par conséquent, son nom d’hôte est
toujours serveur. Vérifiez que la carte réseau du client est débranchée, puis démarrez le client (il
est possible qu’il mette un certain temps à démarrer : ceci est dû à l’absence de connexion Internet).
Comme pour le serveur, désinstallez ensuite cloud-init, puis modifiez le nom de la machine (elle doit
s’appeler client.tpadmin.local).

Photo

9. Vérifiez que les deux machines peuvent communiquer via leur adresse IP, à l’aide de la commande ping.

Photo 
Relatif pas par un / 

10. Modifiez la configuration du serveur pour que l’interface réseau du client reçoive l’IP statique 192.168.100.20 :

