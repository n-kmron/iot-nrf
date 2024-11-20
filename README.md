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

TODO

### Network Discovery

TODO

### La sélection de routeurs

TODO
