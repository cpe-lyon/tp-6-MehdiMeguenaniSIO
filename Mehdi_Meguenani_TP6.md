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
