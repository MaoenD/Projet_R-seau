# # Mémoire sur la gestion des équipements de sécurité et réseaux
### DORGES Guillaume, LIENARD Mathieu, PICARD Gabriel, NDIAYE Oumou Awa
### 1er Décembre 
### YNOV

# Mémoire : Projet de conception et déploiement d'une infrastructure réseau pour un bâtiment

---

## Introduction
Ce travail porte sur la planification et la mise en place d’une infrastructure réseau adaptée à un bâtiment composé de 6 étages, un rez-de-chaussée et 5 sous-sols. L’objectif est de fournir une connectivité efficace pour environ 600 utilisateurs, tout en assurant des performances fiables, un haut niveau de sécurité et une capacité à évoluer en fonction des technologies à venir.

Le document explore les choix techniques retenus, les dimensions des équipements, ainsi que les calculs effectués pour garantir une architecture réseau cohérente et viable. Chaque décision a été prise en tenant compte des contraintes spécifiques du bâtiment et des besoins variés des utilisateurs identifiés, afin de concevoir une solution robuste et adaptée.


## Partie 1 : Analyse des besoins et cadrage du projet

### Présentation du bâtiment
Le projet concerne un bâtiment comprenant 6 étages, un rez-de-chaussée (RDC) et 5 sous-sols, destiné à accueillir 600 utilisateurs avec des équipements connectés variés (à raison de 3 par personne).

### Identification des besoins
Le réseau doit pouvoir connecter **748 équipements** répartis comme suit :
- **Sécurité incendie** : 529 équipements
- **Contrôle d’accès et intrusion** : 89 équipements
- **Vidéosurveillance** : 22 équipements
- **VDI** : 21 équipements
- **GSM** : 87 équipements

Pour plus de détails, un tableau est disponible dans le fichier Travail_Préparatoire.xlsx joint à ce mémoire.

### Exigences techniques
1. **Éviter les points de défaillance uniques (SPF)** :
   - Adoption d'une architecture réseau combinant **topologie full mesh** pour les switchs L3 et **topologie circulaire** avec **partial mesh** pour les switchs L2.
2. **Préparer l'avenir** :
   - Dimensionner le réseau pour supporter une croissance de 30 %.
3. **Isolation des VLANs** :
   - Garantir une sécurité renforcée grâce à une segmentation rigoureuse.

### Contraintes et défis

Le projet vise à concevoir un réseau à la fois fiable, adaptable et capable de répondre aux besoins futurs de l'organisation. Toutefois, plusieurs limites doivent être prises en compte :

---

#### **1. Limites budgétaires**
- **Dépendance à un fournisseur unique** : Le recours exclusif aux équipements HPE Aruba Networking impose un cadre spécifique. Bien que cette solution assure une bonne compatibilité entre les éléments du réseau, elle restreint les options pour réduire les coûts.
- **Gestion optimale des ressources** : Il est crucial d’allouer efficacement les fonds disponibles pour garantir le meilleur équilibre entre coût et performance.

---

#### **2. Exigences de performance et d’évolution**
- **Croissance prévue du réseau** : Le système doit gérer un grand volume de connexions dès sa mise en service (jusqu’à 3 000 appareils), avec la possibilité d’absorber une augmentation de 30 % à moyen terme.
- **Débits nécessaires** : Les besoins en bande passante augmentent en raison d’applications telles que la vidéosurveillance en haute définition ou le Wi-Fi 6E, qui requièrent des transferts rapides et fluides.
- **Adaptabilité** : La conception doit permettre l’ajout progressif de nouveaux équipements (par exemple, bornes Wi-Fi ou VLAN) sans modifications majeures.

---

#### **3. Fiabilité et disponibilité**
- **Continuité de service** : Les services essentiels, comme le contrôle d’accès ou la vidéosurveillance, ne doivent pas être interrompus, exigeant une infrastructure résiliente.
- **Solutions redondantes** : Pour éviter les interruptions dues à des pannes, des équipements et connexions redondants doivent être prévus.
- **Facilité de maintenance** : L’ensemble doit rester simple à gérer et à dépanner afin de limiter les temps d’indisponibilité.

---

#### **4. Sécurité et normes**
- **Isolation des données** : La segmentation via des VLAN permet de sécuriser les échanges entre différents services (bureaux, systèmes de contrôle, etc.).
- **Renforcement des protections** : Des solutions comme les ACL limitent les risques d’accès non autorisés.

---

#### **5. Déploiement et compétences**
- **Respect des délais** : Le réseau doit être opérationnel dans le temps imparti, en respectant les étapes prévues.

---

En somme, le réseau doit concilier efficacité, évolutivité et respect du budget, tout en répondant aux attentes actuelles et futures de l’organisation.

---

## Partie 2 : Conception de l'architecture réseau

### Choix de l'architecture
Les schémas détaillant l'architecture sont disponibles dans le projet Git (**Schémas_Physique.drawio** et **Schémas_Logique.io**).

#### Topologie
1. **Switchs L3 (core)** : Topologie **full mesh** assurant une redondance maximale.
2. **Switchs L2 (accès)** : Topologie **circulaire** avec **partial mesh** pour maintenir un équilibre entre coûts et performance.

#### Dimensionnement du réseau

- **Calcul des besoins en équipements**

Dans le cadre de la conception de l'infrastructure réseau, les besoins en équipements ont été identifiés pour répondre aux contraintes du bâtiment et aux exigences des utilisateurs. Voici le détail des équipements nécessaires :

| Équipement           | Quantité requise |
|-----------------------|------------------|
| **Bornes Wi-Fi**      | 87               |
| **Switch cœur de réseau** | 2                |
| **Switch 24 ports**   | 8                |
| **Switch 48 ports**   | 19               |

Ces équipements permettront de garantir une couverture réseau efficace et une gestion optimale du trafic, en répondant aux besoins de connectivité pour les 600 utilisateurs prévus dans le bâtiment. Le dimensionnement des équipements tient compte des contraintes d'évolutivité, de redondance et de performances attendues.

- **Besoins PoE par étage** : Total estimé à **3 670 W**, réparti selon les besoins des dispositifs (bornes Wi-Fi, caméras, etc.).

### Segmentation VLAN
La segmentation est conçue pour isoler les flux tout en répondant aux besoins des différents services.

| VLAN                         | Subnet IP     | CIDR | Nombre d’adresses | Accès Internet | Accessible autres VLAN | Imprimantes |
|------------------------------|---------------|------|--------------------|----------------|-------------------------|-------------|
| RH                           | 10.0.0.0      | /23  | 510                | X              |                         | X           |
| Comptabilité                 | 10.0.2.0      | /23  | 510                | X              |                         | X           |
| Direction                    | 10.0.10.0     | /23  | 510                | X              | X                       | X           |
| Vidéosurveillance            | 10.0.32.0     | /27  | 30                 |                |                         |             |
| Sécurité incendie            | 10.0.28.0     | /22  | 1022               | X              |                         |             |
| Gestion bâtiment             | 10.0.34.0     | /23  | 510                | X              | X                       | X           |

> **Résumé visuel : VLANs par fonction**

Infrastructure VLAN  
├── RH  
│   ├── Plage IP : 10.0.0.0/23  
│   ├── Protocoles : HTTP/HTTPS, DNS, SMB/IPP  
├── Comptabilité  
│   ├── Plage IP : 10.0.2.0/23  
│   ├── Protocoles : HTTP/HTTPS, DNS, SMB/IPP  
├── Design  
│   ├── Plage IP : 10.0.4.0/23  
│   ├── Protocoles : HTTP/HTTPS, DNS, SMB/IPP  
├── ...  
├── Vidéosurveillance  
│   ├── Plage IP : 10.0.32.0/27  
│   ├── Protocoles : RTSP, HTTPS, Syslog  
└── Gestion bâtiment  
    ├── Plage IP : 10.0.34.0/23  
    ├── Protocoles : HTTP/HTTPS, SNMP, Syslog, Modbus/TCP  

Dans le fichier Travail_Préparatoire.xlsx se trouve tout le détail de la répartition IP

---

## Partie 3 : Mise en œuvre et déploiement

### Besoins en bande passante
Les besoins sont estimés en fonction des utilisateurs et des flux critiques (sécurité, vidéosurveillance). Exemple :
- RDC : **172.54 Gbps**
- Étages 1-6 : Moyenne de **168 Gbps**

### Choix du matériel
1. **Switchs d’accès (Aruba CX 6100)** :
   - **Avantages** : Compatibilité PoE, simplicité de gestion.
   - **Inconvénients** : Limité pour les VLAN complexes.
2. **Bornes Wi-Fi (Aruba AP-635)** :
   - **Avantages** : Wi-Fi 6, haute densité.
   - **Inconvénients** : Coût élevé.
3. **Switchs core (Aruba CX 6300)** :
   - **Avantages** : Haute performance, flexibilité.
   - **Inconvénients** : Consommation énergétique.

Les fiches techniques (datasheets) sont en annexe, et les liens sont fournis en fin de mémoire.

### Access Control Lists (ACL)

Ceci est un échantillon des protocoles autorisé selon les VLAN (cf Travail_Préparatoire.xlsx)

| VLAN          | Protocoles autorisés                                |
|---------------|-----------------------------------------------------|
| RH            | HTTP/HTTPS, DNS, SMB/IPP                           |
| DSI           | HTTP/HTTPS, DNS, SMB/IPP, RDP, SSH, SNMP, Syslog   |
| Vidéosurveillance | RSTP, HTTPS, Syslog                            |


### Tableau explicatif : Protocoles ACL

| **Protocole**     | **Description concise**                                                                                     |
|--------------------|-----------------------------------------------------------------------------------------------------------|
| **HTTP/HTTPS**     | Protocole utilisé pour la communication web, permettant l'accès aux sites et services web sécurisés (HTTPS).|
| **DNS**            | Système de résolution de noms, traduit les noms de domaine en adresses IP.                                |
| **SMB/IPP**        | Protocoles pour le partage de fichiers (SMB) et d'impression (IPP) dans un réseau local.                   |
| **RDP**            | Protocole permettant l'accès distant sécurisé à des ordinateurs ou serveurs.                              |
| **SSH**            | Protocole sécurisé pour l'administration distante des serveurs et le transfert de fichiers.                |
| **SNMP**           | Protocole utilisé pour la gestion et la surveillance des équipements réseau.                               |
| **Syslog**         | Protocole standard pour l'envoi de journaux d'événements vers un serveur central.                          |
| **ICMP**           | Utilisé pour les diagnostics réseau (exemple : commande *ping*).                                           |
| **LDAP**           | Protocole pour interroger et modifier des services d'annuaire comme Active Directory.                      |
| **RADIUS**         | Protocole utilisé pour l'authentification et l'autorisation des utilisateurs réseau.                       |
| **NTP**            | Synchronisation de l'heure des équipements réseau.                                                        |
| **RTSP**           | Protocole pour la diffusion de contenu multimédia en temps réel.                                          |
| **Git**            | Système de contrôle de version pour la gestion de projets de développement.                               |
| **SQL**            | Protocole utilisé                                                                                         |

### Devis

| Description                        | Désignation                                                                                 | Référence | Prix unitaire | Quantité | Total         |
|------------------------------------|---------------------------------------------------------------------------------------------|-----------|---------------|----------|---------------|
| **Switch cœur de réseau**          | HPE Aruba Networking CX 6300M 24-port SFP+ and 4-port SFP56 Switch                         | JL658A    | €8 038,80     | 3        | €24 116,40    |
| **Transformateur**                 | HPE Aruba Networking X371 12VDC 250W 100-240VAC Power Supply                               | JL085A    | €262,40       | 3        | €787,20       |
| **Alimentation**                   | INCLUDED: Power Cord - Europe localization                                                 | JL085A    | incl.         | 3        |               |
| **Switch de distribution 24 ports**| HPE Aruba Networking CX 6100 24G Class4 PoE 4SFP+ 370W Switch                              | JL677A    | €1 405,20     | 8        | €11 241,60    |
| **Alimentation**                   | INCLUDED: Power Cord - Europe localization                                                 | JL677A    | incl.         | 8        |               |
| **Switch de distribution 48 ports**| HPE Aruba Networking CX 6100 48G Class4 PoE 4SFP+ 740W Switch                              | R9Y04A    | €3 214,80     | 19       | €61 081,20    |
| **Alimentation**                   | INCLUDED: Power Cord - Europe localization                                                 | R9Y04A    | incl.         | 19       |               |
| **Borne WI-FI 6E**                 | HPE Aruba Networking AP-635 (RW) Tri-radio 2x2 802.11ax Wi-Fi 6E Internal Antennas Campus AP| R7J27A    | €632,80       | 87       | €55 053,60    |
| **Licence borne Wi-fi**            | Aruba 3Y FC NBD Exch AP-635 SVC  [for R7J27A]                                              | H29YFE    | €77,60        | 87       | €6 751,20     |
| **Licence switch 48 ports**        | Aruba 3Y FC NBD Exch 6100 48G CL4 4SFP+ 740W SVC  [for R9Y04A]                             | H83A5E    | €479,60       | 19       | €9 112,40     |
| **Licence switch 24 ports**        | Aruba 3Y FC NBD Exch 6100 24G CL4 SVC  [for JL677A]                                        | HV1M2E    | €201,60       | 8        | €1 612,80     |
| **Licence switch cœur de réseau**  | Aruba 3Y FC NBD Exch 6300M 24SFP SVC  [for JL658A]                                         | HR4C2E    | €1 024,80     | 3        | €3 074,40     |
| **Configuration switch de distribution**| configuration switch L2                                                                 |           | €60,00        | 10:40:00 | €640,00       |
| **Configuration switch cœur de réseau**| configuration switch L3                                                                 |           | €60,00        | 07:00:00 | €420,00       |
| **Service supplémentaire**         | HPE Aruba Networking Central AP Foundation 5-year Subscription E-STU                      | Q9Y60AAE  | €189,20       | 117      | €22 136,40    |
|                                    |                                                                                             |           |               |   TOTAL       | **€196 027,20** |

Dans ce tableau nous avons aussi inclus un service, le Aruba Network Central qui est une solution réseau basée sur le cloud qui unifie la gestion des infrastructures sans fil, filaires et WAN à travers divers environnements, tels que les campus, les succursales, les centres de données et les sites distants. Elle intègre des fonctionnalités d'analyse et d'alertes intelligentes guidées par l'IA, offrant des informations exploitables pour surveiller, dépanner et améliorer proactivement les performances du réseau.


---

## Documentation et références

| **Documentation**              | **Lien**                                                                    |
|--------------------------------|----------------------------------------------------------------------------|
| Brochure produits Aruba        | https://www.hpe.com/psnow/doc/a00041557fre                                  |
| Switch core                    | https://www.hpe.com/psnow/doc/a00085162enw |
| docu wifi                      | https://www.hpe.com/psnow/doc/PSN1013609618FRFR?jumpid=in_hpesitesearch     |
| switch 48 ports                | https://www.hpe.com/psnow/doc/PSN1013152646FRFR.pdf?jumpid=in_pdp-psnow-dds |
| switch 24 ports                | https://www.hpe.com/psnow/doc/PSN1013152645WWEN.pdf?jumpid=in_pdp-psnow-dds |
| Aruba Networking Central       | https://www.hpe.com/psnow/doc/c05272678.pdf?jumpid=in_pdp-psnow-qs          |


---

## Conclusion
# Conclusion

Ce projet a permis de concevoir et de mettre en place une infrastructure réseau solide, sécurisée et capable d’évoluer dans le temps. Conçue pour répondre aux besoins spécifiques de 600 utilisateurs et pour connecter 748 équipements, cette solution a été élaborée en tenant compte des contraintes propres au bâtiment. La mise en place des VLANs, des règles ACL et d’une topologie pensée pour la redondance garantit une organisation efficace et une fiabilité optimale.

Les équipements sélectionnés, comme les switchs Aruba CX 6100 et CX 6300 ainsi que les bornes Wi-Fi Aruba AP-635, ont été choisis pour leur performance, leur simplicité de gestion et leur capacité à répondre aux exigences techniques en matière de puissance PoE et de bande passante. Une attention particulière a été portée à l’organisation des flux entre les différentes sections du réseau et à l’adressage IP afin d’assurer un fonctionnement optimal.

Grâce à une planification soignée et à l’utilisation de technologies modernes, cette infrastructure est non seulement adaptée aux besoins actuels mais également conçue pour supporter une augmentation significative du nombre d’utilisateurs et de dispositifs connectés. Elle offre une solution performante et flexible, capable de s’adapter aux évolutions futures.
