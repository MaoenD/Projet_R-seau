# # Mémoire sur la gestion des équipements de sécurité et réseaux
### DORGES Guillaume, LIENARD Mathieu, PICARD Gabriel, NDIAYE Oumou Awa
### 1er Décembre 
### YNOV

# Projet de conception et d'implémentation du réseau

## Introduction

Ce mémoire porte sur la conception et la mise en œuvre d'une infrastructure réseau destinée à équiper un bâtiment comprenant 6 étages, un rez-de-chaussée et 5 sous-sols. L'objectif principal de ce projet est de répondre aux besoins de connectivité de 600 utilisateurs tout en garantissant des performances optimales, une sécurité renforcée et une évolutivité permettant d'intégrer des technologies futures. 

Au fil de ce document, les choix techniques, les dimensions matérielles et les calculs nécessaires seront détaillés afin de démontrer la cohérence et la viabilité de l'architecture réseau proposée. Chaque étape de la conception a été menée avec soin pour répondre aux contraintes spécifiques du bâtiment et aux exigences des différents usages identifiés.


# Mémoire : Projet de conception et déploiement d'une infrastructure réseau pour un bâtiment

## Partie 1 : Analyse des besoins et cadrage du projet

### Présentation du bâtiment
Le bâtiment comprend 6 étages, un rez-de-chaussée (RDC) et 5 sous-sols, totalisant une capacité d'accueil pour 600 utilisateurs et leurs équipements connectés.

### Identification des besoins
Le réseau doit permettre de connecter un total de **748 équipements** répartis comme suit :
- **Sécurité incendie** : 529 équipements
- **Contrôle d’accès et intrusion** : 89 équipements
- **Vidéosurveillance** : 22 équipements
- **VDI** : 21 équipements
- **GSM** : 87 équipements

Pour plus de détails, un tableau récapitulatif est disponible dans un fichier Google Sheets joint à ce mémoire.

### Exigences techniques
Le réseau devra respecter les critères suivants :
- Éviter tout point de défaillance unique (Single Point of Failure, SPF) grâce à une topologie combinant **full mesh** pour les switchs de niveau 3 et **circulaire** pour les switchs de niveau 2, avec partial mesh en extrémités.
- Supporter un agrandissement de 30 % de la capacité initiale.
- Sécuriser les flux en isolant les VLANs, un point qui sera abordé dans une partie dédiée.

### Contraintes et enjeux
Le projet vise à offrir des performances optimales tout en maîtrisant les coûts. Cependant, le fournisseur des équipements est imposé, ce qui limite les options de négociation tarifaire.

---

## Partie 2 : Conception de l'architecture réseau

### Choix de l'architecture
Les schémas détaillant l'architecture physique et logique sont disponibles dans le projet Git sous les noms **Schémas_Physique.drawio** et **Schémas_Logique.io**. Les principales décisions sont :
- **Switchs L3 (niveau core)** : Topologie **full mesh** pour garantir une redondance maximale.
- **Switchs L2 (niveau d’accès)** : Topologie **circulaire** avec **partial mesh** pour sécuriser les extrémités et maintenir un équilibre entre coûts et performance.

### Dimensionnement du réseau

#### Nombre d'équipements par étage :
| Étages | SS5 | SS4 | SS3 | SS2 | SS1 | RDC | ET1 | ET2 | ET3 | ET4 | ET5 | ET6 |
|--------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| Équipements | 15  | 21  | 30  | 35  | 84  | 127 | 70  | 82  | 81  | 82  | 74  | 47  |

#### Besoins PoE (en watts) :
| Étages | SS5  | SS4  | SS3  | SS2  | SS1  | RDC  | ET1  | ET2  | ET3  | ET4  | ET5  | ET6  |
|--------|------|------|------|------|------|------|------|------|------|------|------|------|
| PoE    | 73   | 103  | 108.5| 190  | 287  | 597  | 479  | 484  | 482  | 485  | 462  | 400  |

#### Calcul du nombre de switchs :
| Étages | SS5 | SS4 | SS3 | SS2 | SS1 | RDC | ET1 | ET2 | ET3 | ET4 | ET5 | ET6 | TOTAL |
|--------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-------|
| 24 ports | 1   | 0   | 0   | 0   | 1   | 1   | 0   | 1   | 1   | 1   | 1   | 1   | 8     |
| 48 ports | 0   | 1   | 1   | 1   | 2   | 3   | 2   | 2   | 2   | 2   | 2   | 1   | 19    |

### Besoins en bande passante (en Gbps) :
| Étages | SS5  | SS4  | SS3  | SS2  | SS1  | RDC  | ET1  | ET2  | ET3  | ET4  | ET5  | ET6  |
|--------|------|------|------|------|------|------|------|------|------|------|------|------|
| Bande passante | 11   | 39   | 83.2 | 56.4 | 129.8| 172.54| 40.5 | 169.6| 168.6| 169.7| 150.8| 31.9 |

Ces chiffres montrent la capacité requise pour chaque étage afin d’assurer la fluidité du trafic réseau.

### Segmentation VLAN
## Plages IP

| VLAN                                 | Accès Internet | Accessible autres VLAN | Imprimantes | Subnet IP   | CIDR | Nombre d’adresses |
|-------------------------------------|----------------|-------------------------|-------------|-------------|------|--------------------|
| RH                                  | X              |                        | X           | 10.0.0.0    | /23  | 510                |
| Comptabilité                        | X              |                        | X           | 10.0.2.0    | /23  | 510                |
| Design                              | X              |                        | X           | 10.0.4.0    | /23  | 510                |
| Logistique                          | X              |                        | X           | 10.0.6.0    | /23  | 510                |
| Imprimantes                         | X              | X                       | X           | 10.0.8.0    | /23  | 510                |
| Direction                           | X              | X                       | X           | 10.0.10.0   | /23  | 510                |
| DSI                                 | X              | X                       | X           | 10.0.12.0   | /23  | 510                |
| R&D                                 | X              |                        | X           | 10.0.14.0   | /23  | 510                |
| Dev                                 | X              | X                       | X           | 10.0.16.0   | /23  | 510                |
| Data                                | X              | X                       | X           | 10.0.18.0   | /23  | 510                |
| Conception                          | X              |                        | X           | 10.0.20.0   | /23  | 510                |
| Invités Wi-Fi                       | X              |                         |             | 10.0.22.0   | /23  | 510                |
| Contrôle d'accès, Détection intrusion et vidéophonie |                |                         |             | 10.0.25.0   | /25  | 126                |
| Sécurité Incendie                   | X              |                         |             | 10.0.28.0   | /22  | 1022               |
| Vidéosurveillance                   |                |                         |             | 10.0.32.0   | /27  | 30                 |
| Système audio                       |                |                         |             | 10.0.32.32  | /28  | 14                 |
| Gestion bâtiment                    | X              | X                       | X           | 10.0.34.0   | /23  | 510                |
| VIDE                                |                |                         |             | 10.0.36.0   | /23  | 510                |
| VIDE                                |                |                         |             | 10.0.38.0   | /23  | 510                |
| VIDE                                |                |                         |             | 10.0.40.0   | /23  | 510                |
| VIDE                                |                |                         |             | 10.0.42.0   | /23  | 510                |

---

## Access Control Lists (ACL)

| VLAN                                  | Protocoles autorisés                                              |
|--------------------------------------|---------------------------------------------------------------------------------------------|
| RH                                   | HTTP/HTTPS, DNS, SMB/IPP                                          |
| Comptabilité                         | HTTP/HTTPS, DNS, SMB/IPP                                          |
| Design                               | HTTP/HTTPS, DNS, SMB/IPP                                          |
| Logistique                           | HTTP/HTTPS, DNS, SMB/IPP                                          |
| Imprimantes                          | SMB, IPP, HTTP/HTTPS                                             |
| Direction                            | HTTP/HTTPS, DNS, SMB/IPP, RDP, SNMP                              |
| DSI                                  | HTTP/HTTPS, DNS, SMB/IPP, RDP, SSH, SNMP, Syslog, ICMP, LDAP, RADIUS, NTP, RTSP, Modbus/TCP |
| R&D                                  | HTTP/HTTPS, DNS, SMB/IPP, Git, SSH                               |
| Dev                                  | HTTP/HTTPS, DNS, SMB/IPP, Git, SSH, RDP, VDI                     |
| Data                                 | HTTP/HTTPS, DNS, SMB/IPP, RDP, SSH, SQL, SNMP, BACnet, Modbus/TCP |
| Conception                           | HTTP/HTTPS, DNS, SMB/IPP                                          |
| Invités Wi-Fi                        | HTTP/HTTPS, DNS                                                  |
| Contrôle d'accès, Détection intrusion et vidéophonie | RSTP, HTTPS, Syslog                                              |
| Sécurité Incendie                    | HTTPS, Syslog                                                    |
| Vidéosurveillance                    | RSTP, HTTPS, Syslog                                              |
| Système audio                        | HTTPS                                                            |
| Gestion bâtiment                     | HTTP/HTTPS, SNMP, Syslog, RADIUS, NTP, RTSP, Modbus/TCP, BACnet/IP |

---

## Explication des protocoles

| Protocole       | Explication courte                                                                 |
|------------------|-----------------------------------------------------------------------------------|
| HTTP/HTTPS      | Protocoles pour la navigation web sécurisée.                                      |
| DNS             | Résolution de noms de domaine en adresses IP.                                     |
| SMB/IPP         | Protocoles pour le partage de fichiers et l'impression en réseau.                 |
| RDP             | Protocole pour la prise en main à distance de machines Windows.                   |
| SSH             | Connexion sécurisée pour l'administration à distance.                             |
| SNMP            | Surveillance et gestion des équipements réseau.                                  |
| Syslog          | Collecte des journaux système pour la surveillance et le diagnostic.              |
| ICMP            | Utilisé pour le diagnostic réseau (exemple : commandes ping).                     |
| LDAP            | Service d'annuaire pour l'authentification des utilisateurs.                      |
| RADIUS          | Authentification et contrôle d'accès réseau.                                      |
| NTP             | Synchronisation des horloges des équipements.                                     |
| RTSP            | Diffusion en streaming pour les caméras de vidéosurveillance.                     |
| Modbus/TCP      | Communication pour la gestion des systèmes industriels.                           |
| BACnet          | Protocole utilisé pour les systèmes de gestion de bâtiments (GTC).               |
| Git             | Système de contrôle de version pour les développeurs.                             |
| VDI             | Infrastructure pour la virtualisation des postes de travail.                      |

---

### Choix du matériel
- **Switchs d’accès : Aruba CX 6100 (24/48 ports)**  
  Avantages : Compatibilité PoE, simplicité de gestion, rapport qualité/prix.  
  Inconvénients : Limité en capacités avancées pour les VLAN complexes.
- **Bornes Wi-Fi : Aruba AP-635**  
  Avantages : Haute densité, support du Wi-Fi 6.  
  Inconvénients : Coût élevé.
- **Switchs core : Aruba CX 6300**  
  Avantages : Performance élevée, redondance, gestion avancée des VLANs.  
  Inconvénients : Consommation énergétique plus importante.

Les datasheets sont disponibles en annexe, avec des liens en fin de mémoire.

---
