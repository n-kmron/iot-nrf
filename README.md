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
