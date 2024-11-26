# Mémoire : Projet de conception et déploiement d'une infrastructure réseau pour un bâtiment

---

## Partie 1 : Analyse des besoins et cadrage du projet

### Présentation du bâtiment
Le projet concerne un bâtiment comprenant 6 étages, un rez-de-chaussée (RDC) et 5 sous-sols, destiné à accueillir 600 utilisateurs avec des équipements connectés variés.

### Identification des besoins
Le réseau doit connecter **748 équipements** répartis comme suit :
- **Sécurité incendie** : 529 équipements
- **Contrôle d’accès et intrusion** : 89 équipements
- **Vidéosurveillance** : 22 équipements
- **VDI** : 21 équipements
- **GSM** : 87 équipements

Pour plus de détails, un tableau détaillé est disponible dans le fichier Google Sheets joint à ce mémoire.

### Exigences techniques
1. **Éviter les points de défaillance uniques (SPF)** :
   - Adoption d'une architecture réseau combinant **topologie full mesh** pour les switchs L3 et **topologie circulaire** avec **partial mesh** pour les switchs L2.
2. **Préparer l'avenir** :
   - Dimensionner le réseau pour supporter une croissance de 30 %.
3. **Isolation des VLANs** :
   - Garantir une sécurité renforcée grâce à une segmentation rigoureuse.

### Contraintes et enjeux
L'objectif est de concevoir un réseau performant et évolutif tout en respectant des contraintes budgétaires strictes imposées par le choix exclusif d’un fournisseur.

---

## Partie 2 : Conception de l'architecture réseau

### Choix de l'architecture
Les schémas détaillant l'architecture sont disponibles dans le projet Git (**Schémas_Physique.drawio** et **Schémas_Logique.io**).

#### Topologie
1. **Switchs L3 (core)** : Topologie **full mesh** assurant une redondance maximale.
2. **Switchs L2 (accès)** : Topologie **circulaire** avec **partial mesh** pour maintenir un équilibre entre coûts et performance.

#### Dimensionnement du réseau
- **Nombre d'équipements par étage** : Voir tableau détaillé en annexe.
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
| VLAN          | Protocoles autorisés                                |
|---------------|-----------------------------------------------------|
| RH            | HTTP/HTTPS, DNS, SMB/IPP                           |
| DSI           | HTTP/HTTPS, DNS, SMB/IPP, RDP, SSH, SNMP, Syslog   |
| Vidéosurveillance | RSTP, HTTPS, Syslog                            |

---

## Documentation et références

| **Documentation**              | **Lien**                                                                    |
|--------------------------------|----------------------------------------------------------------------------|
| Brochure produits Aruba        | https://www.hpe.com/psnow/doc/a00041557fre                                  |
| docu switch                    | https://www.hpe.com/psnow/doc/PSN1013152646FRFR.pdf?jumpid=in_pdp-psnow-dds |
| docu wifi                      | https://www.hpe.com/psnow/doc/PSN1013609618FRFR?jumpid=in_hpesitesearch     |

---

## Conclusion
Le projet présenté garantit une infrastructure réseau performante, évolutive et sécurisée tout en respectant les contraintes imposées. Les choix techniques sont justifiés par des données chiffrées et une conception solide, appuyée par des documents et visualisations en annexe.
