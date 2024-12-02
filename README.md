# Threads
Discover Thread ipv6 protocol with NRF-Dongle

## Objectives 

Do a report with observations and send it to `a.tillieux@helmo.be` the last week

## Theory in french

### Concepts clés sur les réseaux Threads

Thread est un protocole de communication sans fil, conçu pour l'IOT (ipv6)

#### Fiable, sécurisé et optimisé (faible consommation d'énergie, ...)
  
#### Réseau maillé

Chaque appareil peut servir de noeud pour acheminer les messages
* les avantages du réseau maillé sont que :
  - le réseau s'auto-réorganise pour maintenir la communication
  - gère mieux les obstacles et interférences
 
#### Consommation d'énergie 

Conçu pour les appareils sur batterie et optimise l'autonomie en réduisant les communications redondantes et les cycles de réveil inutils

#### Sécurité

Utilise le chiffrement AES end-to-end et chaque appareil doit s'authentifier pour rejoindre le réseau

#### Scalable 

Supporte des centaines de noeuds 

#### Interopérabilité

S'intègre facilement avec d'autres réseaux IP

Les noeuds sont coupés en 2 roles sur Thread:

##### Les routeurs 

* transfèrent les paquets aux périphériques
* fournissent des services de mise en service sécurisés pour les nouveaux périphériques
* Maintient son émetteur-récepteur activé tout le temps

##### End devices

* communiquent avec un seul routeur
* ne transmettent pas de paquet à d'autres pérhiphériques réseau
* peuvent désactiver leur émetteur-récepteur pour économiser de la batterie

#### Les types de deivces

##### FTP (full thread device)

* radio toujours allumée
* subscribe à l'adresse multicast de tous les routeurs
* il existe 3 types de FTP : les routeurs, les end devices éligibles à devenir routeur (REED) et les end devices qui ne peuvent pas devenir routeur (FED)

##### Minimal thread device

* ne se subscribe pas aux adresses multicast de tous les routeurs
* transfère tous les messages vers son parent
* il en existe 2 types : les minimal end devices (MED) dont l'émetteur-récepteur est toujours on et qui ne doit pas interroger son parent et les sleepy end devices (SED) dont l'émetteur-récepteur est normalement désactivé et se réveille de temps en temps pour interroger son parent

#### Upgrade et downgrade

Quand un REED (FTP) est le seul node voulant rejoindre un réseau Thread, il peut s'upgrade lui-même au rang de routeur.

Quand un routeur n'a aucun enfant, alors il downgrade lui-même au rang de end-device

Le Thread leader est un routeur responsable de gérer les routeurs dans un réseau Thread. Il est dynamiquement élu et il n'y en a qu'un seul par réseau.

Un routeur de frontière (border router) est un routeur capable de transmettre les informations entre un réseau Thread et un réseau non Thread (ex: Wifi)

#### Les partitions

Un réseau Thread peut être coupé en partitions lorsqu'un groupe de devices ne peuvent pas communiquer avec un autre groupe.

Chaque partition fonctionne comme un réseau Thread distinct, avec son propre leader, router assignment mais ont les mêmes niveaux et credentials de sécurité.


### L'IPV6 avec Thread

Il existe trois portées dans un réseau Thread pour l'adressage en unicast :

Link-Local : toutes les interfaces accessibles par une seule transmission radio
Mesh-Local : toutes les interfaces accessibles au sein du même réseau Thread
Global : toutes les interfaces accessibles depuis l'extérieur d'un réseau Thread
Les deux premières portées correspondent aux préfixes désignés par un réseau Thread. Link-Local a le préfixe fe80::/16, tandis que Mesh-Local a le préfixe fd00::/8.

Plusieurs adresses IPv6 en monodiffusion (unicast) qui identifient un seul périphérique Thread. Chacune a une fonction différente en fonction de la portée et du cas d'utilisation.

#### The Routing Locator (RLOC).

Un RLOC est généré : tous les périphériques se voient attribuer un ID de routeur et un ID d'enfant. Chaque routeur conserve une table de tous ses enfants, dont la combinaison identifie de manière unique un périphérique dans la topologie. Par exemple, considérons les nœuds mis en surbrillance dans la topologie suivante, où le numéro dans un routeur (pentagone) est l'ID de routeur et le numéro dans un périphérique final (cercle) est l'ID d'enfant :

L'ID de routeur de chaque enfant correspond à son parent (routeur). Étant donné qu'un routeur n'est pas un enfant, l'ID d'enfant d'un routeur est toujours 0. Ensemble, ces valeurs sont uniques pour chaque périphérique du réseau Thread et sont utilisées pour créer le RLOC16, qui représente les 16 derniers bits du RLOC.

### Network Discovery

Les réseaux de threads sont identifiés par trois identifiants uniques :

ID de réseau personnel (PAN ID) sur 2 octets
ID de réseau personnel étendu (XPAN ID) sur 8 octets
Un nom de réseau lisible par l'homme

Pour créer un nouveau réseau, il sélectionne le canal le moins occupé et un ID PAN non utilisé par d'autres réseaux, puis devient un routeur et s'élit lui-même comme leader. Cet appareil envoie des messages d'annonce MLE à d'autres appareils 802.15.4 pour les informer de son état de liaison et répond aux demandes de balise des autres appareils Thread effectuant une analyse active.

Pour rejoindre un réseau existant, il configure son canal, son ID PAN, son ID XPAN et son nom de réseau pour qu'ils correspondent à ceux du réseau cible via la mise en service des threads, puis passe par le processus de connexion MLE pour se connecter en tant qu'enfant (appareil final). Ce processus est utilisé pour les liens enfant-parent.

### La sélection de routeurs

Les routeurs doivent former un Connected Dominating Se (CDS), ce qui signifie :

Tout routeur d'un réseau Thread peut atteindre n'importe quel autre routeur en restant entièrement dans l'ensemble de routeurs.

Chaque périphérique final d'un réseau Thread est directement connecté à un routeur.

Un algorithme distribué gère le CDS, ce qui garantit un niveau minimum de redondance. Chaque périphérique se connecte initialement au réseau en tant que périphérique final (enfant). À mesure que l'état du réseau de threads change, l'algorithme ajoute ou supprime des routeurs pour maintenir le CDS.
