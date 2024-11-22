# # Mémoire sur la gestion des équipements de sécurité et réseaux
### DORGES Guillaume, LIENARD Mathieu, PICARD Gabriel, NDIAYE Oumou Awa
### 1er Décembre 
### YNOV

# Projet de conception et d'implémentation du réseau

## Introduction

Ce document présente la conception, les choix techniques, les calculs et les équipements sélectionnés pour un projet réseau visant à connecter 600 utilisateurs, avec une approche structurée et optimisée pour les besoins actuels et futurs de l'organisation.

## Dimensionnement des adresses IP

### Calcul des besoins en adresses IP

- **Nombre d'utilisateurs** : 600 personnes.
- **Dispositifs par utilisateur** : 3 appareils (PC, smartphone, tablette).
- **Total** : 600 × 3 = **1800 appareils connectés**.
- **Allocation par service** : Environ 100 utilisateurs par service, soit 300 adresses IP par service.
- **Réseau** :
  - Pour éviter la saturation, une plage plus large a été choisie.
  - Utilisation de sous-réseaux en /24 (à 510 adresses utilisables).

### Tableau de répartition des sous-réseaux

| **Service**                                | **Sous-réseau** | **CIDR** | **Adresses disponibles** |
|-------------------------------------------|------------------|----------|--------------------------|
| RH                                         | 10.0.1.0         | /24      | 510                      |
| Compatibilité                              | 10.0.2.0         | /24      | 510                      |
| Design                                     | 10.0.3.0         | /24      | 510                      |
| Logistique                                 | 10.0.4.0         | /24      | 510                      |
| Imprimantes                                | 10.0.5.0         | /24      | 510                      |
| Direction                                  | 10.0.6.0         | /24      | 510                      |
| DSI                                        | 10.0.7.0         | /24      | 510                      |
| R&D                                        | 10.0.8.0         | /24      | 510                      |
| Développement (Dev)                       | 10.0.9.0         | /24      | 510                      |
| Data                                       | 10.0.10.0        | /24      | 510                      |
| Conception                                 | 10.0.11.0        | /24      | 510                      |
| Invités Wi-Fi                              | 10.0.12.0        | /24      | 510                      |
| Contrôle d’accès                         | 10.0.13.0        | /24      | 510                      |
| Vidéosurveillance                         | 10.0.14.0        | /24      | 510                      |
| Gestion bâtiment                          | 10.0.15.0        | /24      | 510                      |

## Choix des équipements

### Critères de sélection
Les équipements ont été choisis en fonction des besoins actuels et futurs en termes de performance, fiabilité et budget. Voici les équipements retenus :

#### Commutateurs (Switchs)
- Modèle : **Aruba CX 6100** pour les étages et **Aruba CX 6200/6100** pour le sous-sol.
- Avantages :
  - Compatible PoE pour alimenter les appareils tels que caméras ou points d'accès Wi-Fi.
  - Hautes performances pour la gestion du trafic local.

#### Points d'accès Wi-Fi
- Modèle : **Aruba AP-635**.
- Fonctionnalités :
  - Compatible Wi-Fi 6E pour des performances accrues.
  - Couverture optimale pour les environnements denses.

#### Routeur
- Modèle : **Aruba 7205**.
- Justification :
  - Capacité élevée de gestion du trafic entrant/sortant.
  - Sécurité et gestion centralisée des connexions.

#### Cœur de réseau (Core Switch)
- Modèle : **Aruba CX 6400**.
- Rôle :
  - Gestion des connexions principales.
  - Assure la redondance et la haute disponibilité.

### Schéma de connexion des équipements
Les équipements sont connectés en fonction de leur emplacement (RDC, sous-sol, étages). Le câblage utilise :
- **Catégorie 6/7** pour les connexions proches.
- **OM5** pour les connexions longues ou critiques.

## Calculs PoE (Power over Ethernet)

Les appareils alimentés par PoE comprennent les caméras de vidéosurveillance, les points d'accès Wi-Fi et certains dispositifs IoT.

### Tableau PoE
| **Type d'équipement**         | **Nombre par étage** | **Puissance requise (Watts)** |
|-------------------------------|-----------------------|--------------------------------|
| Points d'accès Wi-Fi         | 72                    | 15 W                          |
| Caméras de sécurité         | 50                    | 30 W                          |
| Contrôle d’accès           | 35                    | 25 W                          |

### Capacité PoE totale
La capacité totale des switchs choisis couvre largement les besoins en PoE pour tous les équipements alimentés.

## Bande passante

Bien que le calcul de bande passante n'ait pas été réalisé en détail, les équipements choisis disposent d'une capacité de transfert largement suffisante pour supporter une utilisation intensive par 600 utilisateurs, avec une croissance potentielle de la demande.

- **Switchs** : Jusqu'à 10 Gbps pour la dorsale.
- **Points d'accès Wi-Fi** : Compatible avec des connexions à haute densité.

## Documentation et références

| **Documentation**              | **Lien**                                                                                   |
|--------------------------------|--------------------------------------------------------------------------                  |
| Schémas logique                | [Lien vers le projet GitHub](https://github.com/MaoenD/Projet_R-seau)                      |
| Brochure produits Aruba        | [Lien brochure](https://www.securewirelessworks.com/JL675A.asp)                            |
| docu switch                    | [Lien switches](https://www.hpe.com/psnow/doc/PSN1013152646FR.pdf?jumpid=in_pdp-psnow-dds) |
| docu router                    | [Lien router](https://www.hpe.com/psnow/doc/PSN1009434920FR?jumpid=in_hpesitesearch)       |
| docu wifi                      | [Lien wifi](https://www.hpe.com/psnow/doc/PSN1013609618FR?jumpid=in_hpesitesearch)         |