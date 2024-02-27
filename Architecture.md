# Architecture Réseau Cisco Packet Tracer

Cette documentation décrit l'architecture réseau conçue avec Cisco Packet Tracer, illustrant la configuration d'un environnement réseau composé de plusieurs VLANs, un routeur-on-a-stick pour la gestion inter-VLAN, et une connexion à Internet via NAT, avec des mesures de sécurité.

## Configuration du Réseau

### Switch 1 (S1) - VLAN 10 (Admin)

- **Composants Connectés**:
    - 2 Serveurs:
        + Serveur FTP
        + Serveur DHCP
    - 2 Ordinateurs de bureau
- **VLAN**: 10 (Admin)
- **Connectivité**: Tous les appareils connectés au Switch 1 sont membres du VLAN 10 ainsi qu'une connexion Internet via le routeur NAT Dynamique.
- **Sécurité**:
    - Port Security activé pour limiter le nombre de MAC adresses.
    - Dynamic ARP Inspection (DAI) pour prévenir le ARP spoofing.
    - DHCP Snooping pour protéger contre les attaques sur le serveur DHCP.

### Routeur-on-a-Stick

- **Fonction**: Crée la connexion inter-VLAN entre les VLAN 10, 20, et 30, permettant la communication entre les différents segments de réseau en utilisant OSPF et en étant le BDR avec le routeur NAT_Router le DR.

### Switch 2 (S2) - VLAN 20 (Finance)

- **Composants Connectés**:
    - 2 Ordinateurs de bureau
- **VLAN**: 20 (Finance)
- **Connectivité**: Relié au Switch 1 (S1) et permet la communication avec le VLAN 20 ainsi qu'une connexion Internet via le routeur NAT Dynamique.
- **Sécurité**:
    - Port Security activé.
    - Dynamic ARP Inspection (DAI).
    - DHCP Snooping.

### Switch 3 (S3) - VLAN 30 (IT) et VLAN 40 (Guest)

- **Composants Connectés**:

    - 2 Ordinateurs de bureau dans le VLAN 30 (IT)
    - Routeur SOHO connecté à un Modem DSL, à son tour connecté à :
        + 1 Laptop dans le VLAN 40 (Guest)
        + 1 Smartphone dans le VLAN 40 (Guest)

- **VLAN**: 30 (IT)
- **VLAN 40 (Guest)**: Isolé, sans communication inter-VLAN avec les autres VLANs pour renforcer la sécurité et l'isolation des invités.
- **Connectivité**: 
    - VLAN 30: Connecté au Switch 2 (S2) et assure la communication au sein du VLAN 30 ainsi qu'une connexion Internet via le routeur NAT Dynamique.
    - VLAN 40: Fournit un accès Internet isolé aux invités via le routeur SOHO, sans possibilité de communication avec les autres VLANs pour une sécurité accrue.
- **Sécurité**:
    - Port Security activé.
    - Dynamic ARP Inspection (DAI).
    - DHCP Snooping.

## Schéma du Réseau
![Schéma cisco packet tracer](https://raw.githubusercontent.com/MalikSploit/Architecture_CCNA/main/Maquette.png)

## Configuration de Sécurité

Les mesures suivantes ont été mises en place pour sécuriser le réseau :

- **Port Security**: Limite le nombre de MAC adresses sur les ports pour prévenir les attaques de type MAC flooding.
- **Dynamic ARP Inspection (DAI)**: Empêche le ARP spoofing en vérifiant les paquets ARP contre une table de confiance.
- **DHCP Snooping**: Protège contre les attaques visant à usurper le serveur DHCP en filtrant les messages DHCP non fiables.
- **Désactivation du CDP sur le port connecté au routeur ISP**: Empêche la divulgation d'informations sur le réseau aux dispositifs non autorisés en désactivant CDP sur l'interfaces connectée au routeur ISP.
