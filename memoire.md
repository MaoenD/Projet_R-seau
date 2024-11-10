# # Mémoire sur la gestion des équipements de sécurité et réseaux
### DORGES Guillaume, LIENARD Mathieu, PICARD Gabriel, NDIAYE Oumou Awa
### 1er Décembre 
### YNOV

## 1. Introduction

Ce mémoire présente l'analyse des besoins en équipements pour un bâtiment multi-étages. Il couvre la gestion des équipements de sécurité incendie, de contrôle d'accès, de vidéosurveillance, et d'autres infrastructures réseau. Le but est de détailler les choix d'équipements, de vérifier le PoE (Power over Ethernet), de calculer les quantitatifs IP, et d'assurer la bande passante adéquate.

## 2. Contexte et Objectifs

Le bâtiment comporte plusieurs étages (RDC, SS1 à SS5, ET1 à ET6). Chaque étage nécessite des équipements spécifiques pour répondre aux besoins de sécurité, d'infrastructure réseau, et de gestion des connexions réseau. Le tableau ci-dessous présente les équipements répartis par étage.

## 3. Méthodologie

### 3.1. Catégorisation des Équipements

Les équipements sont classés en plusieurs catégories :

- **Sécurité incendie** : Détecteurs automatiques, déclencheurs manuels, diffuseurs sonores, etc.
- **Contrôle d'accès et intrusion** : Lecteurs de badges, détecteurs de bris de vitre, détecteurs de présence.
- **Vidéosurveillance** : Caméras fixes extérieures et intérieures.
- **VDI (Infrastructure réseau)** : Prises RJ45 et autres équipements réseau.
- **GSM (Bornes Wi-Fi)** : Bornes Wi-Fi pour couverture réseau.
- **GTC (Gestion Technique de Confort)** : Modules de gestion de confort.

### 3.2. Calcul des Quantitatifs IP

Les quantitatifs IP sont calculés en fonction des équipements réseau (prises RJ45 et bornes Wi-Fi). En voici la répartition :

| Équipement                                 | Quantité Totale |
|--------------------------------------------|-----------------|
| Prises RJ45 / 2 Prises RJ45                | 16              |
| Bornes Wi-Fi                               | 15              |
| Caméras de vidéosurveillance (ext. et int.) | 22              |

Les adresses IP nécessaires pour chaque type d'équipement sont prises en compte dans le calcul de la capacité du réseau.

### 3.3. Vérification du PoE et de la Bande Passante

#### PoE (Power over Ethernet)
Les équipements nécessitant de l'alimentation par PoE sont principalement les caméras de vidéosurveillance et les bornes Wi-Fi. Le calcul est basé sur la consommation en énergie de chaque appareil et la capacité des switches à fournir cette puissance.

- **Caméras de vidéosurveillance** : Chaque caméra consomme environ 15W.
- **Bornes Wi-Fi** : Chaque borne consomme environ 10W.

Les switches doivent être capables de délivrer suffisamment de puissance pour ces appareils.

#### Bande Passante
Les équipements qui consomment de la bande passante sont :
- **Caméras de vidéosurveillance** : chaque caméra consomme environ 4 à 6 Mbps, en fonction de la qualité de l'image.
- **Bornes Wi-Fi** : consomment environ 10 à 20 Mbps, selon le trafic.

Nous avons dimensionné le réseau pour garantir une bande passante suffisante sur tous les étages.

## 4. Choix des Équipements

### 4.1. Sécurité Incendie

Les équipements de sécurité incendie ont été choisis en fonction de leur efficacité à détecter les risques. Voici les choix spécifiques pour chaque type :

- **Détecteurs automatiques SGX** : 263 unités réparties sur l'ensemble du bâtiment pour assurer une couverture optimale.
- **Diffuseurs sonores** : 62 unités pour alerter rapidement en cas d'incendie.
- **Flash lumineux** : 123 unités pour signaler visuellement un danger.

### 4.2. Contrôle d'Accès et Intrusion

Les équipements de contrôle d'accès sont essentiels pour sécuriser les zones sensibles :

- **Lecteurs de badges** : 18 unités réparties principalement sur le RDC et dans les zones sensibles.
- **Détecteurs d'intrusion Radar** : 13 unités pour détecter les mouvements non autorisés.
- **Détecteurs de bris de vitre** : 7 unités pour surveiller les fenêtres et points d'entrée.

### 4.3. Vidéosurveillance

Les caméras de vidéosurveillance sont stratégiquement placées pour assurer une couverture complète :

- **Caméras fixes extérieures** : 9 unités placées principalement à l'extérieur du bâtiment pour surveiller les accès.
- **Caméras fixes intérieures** : 13 unités placées dans les zones sensibles à l'intérieur du bâtiment.

### 4.4. VDI (Infrastructure Réseau)

Les équipements réseau comprennent des prises RJ45 et des bornes Wi-Fi :

- **Prises RJ45** : 16 prises installées principalement dans les bureaux et espaces nécessitant des connexions réseau fixes.
- **Bornes Wi-Fi** : 15 bornes réparties pour assurer une couverture Wi-Fi complète dans l'ensemble du bâtiment.

## 5. Vérification du PoE et de la Bande Passante

### 5.1. PoE
Nous avons vérifié que les switches PoE sont capables de délivrer la puissance nécessaire pour les caméras et les bornes Wi-Fi. Voici un récapitulatif des besoins PoE :

- **Caméras de vidéosurveillance** : 15W par caméra.
- **Bornes Wi-Fi** : 10W par borne.

Les switches PoE+ sont nécessaires pour fournir cette puissance.

### 5.2. Bande Passante
La bande passante nécessaire a été estimée en fonction du nombre d'équipements connectés et du type de trafic :

- **Caméras extérieures et intérieures** : 4 à 6 Mbps par caméra.
- **Bornes Wi-Fi** : 10 à 20 Mbps par borne.

Un switch de 1 Gbps par étage est recommandé pour assurer une bande passante suffisante.

## 6. Datasheets des Équipements Choisis

### 6.1. Détecteur automatique SGX

**Caractéristiques** :
- **Type** : Détecteur automatique d’incendie.
- **Technologie** : Détection de fumée optique.
- **Consommation** : 8 mA.
- **Installation** : Plafond.



### 6.2. Caméra Fixe Extérieure

**Caractéristiques** :
- **Type** : Caméra de vidéosurveillance fixe extérieure.
- **Résolution** : 4K UHD.
- **Consommation PoE** : 15W.
- **Angle de vue** : 120°.


### 6.3. Borne Wi-Fi

**Caractéristiques** :
- **Type** : Borne Wi-Fi de type 802.11ac.
- **Fréquence** : 2.4 GHz / 5 GHz.
- **Consommation PoE** : 10W.
- **Capacité** : Jusqu’à 500 clients simultanés.

## 7. Conclusion

Ce mémoire présente une analyse complète des équipements nécessaires pour la gestion des infrastructures de sécurité et réseau dans un bâtiment multi-étages. La répartition des équipements, la vérification du PoE et de la bande passante, ainsi que le choix des équipements ont été effectués en fonction des besoins spécifiques du projet.

## 8. Annexes

- [Schémas logiques du réseau](https://github.com/MaoenD/Projet_R-seau)
- [Brochure sur les produits et solutions HPE Aruba Networking](https://www.securewirelessworks.com/JL675A.asp)
- [Documentation sur le Switch Aruba JL675A](https://www.securewirelessworks.com/JL675A.asp)
- [Documentation sur le Router Aruba 7205 Mobility Controller](https://example.com/doku_router_7205)
- [Documentation sur la Borne Wi-Fi Aruba 635 - Wi-Fi 6E](https://example.com/doku_wifi_635)
