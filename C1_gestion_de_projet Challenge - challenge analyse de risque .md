
# challenge E03

## Énoncé

### Contexte

Vous êtes responsable de l'informatique au sein d'un campus de formation professionnelle (en présentiel 😁).

Le campus compte en permanence environ 500 personnes, entre les salariés (une quinzaine), les formateurs (freelances, formateurs occasionnels) et les apprenants (formation continue et alternance).

La direction vous demande de moderniser l’infrastructure IT du campus pour accueillir de nouveaux services numériques : serveurs fichiers, NAS, firewall, VLAN et accès sécurisé Wi-Fi.

Dans votre service, vous accueillez actuellement un alternant.

### Consignes

Vous avez créé la note de cadrage du projet ainsi que le WBS.

Aujourd'hui on s'attaque à l'analyse des risques !

1. Listez au moins 10 risques du projet (technique, humain, organisationnel)
2. Évaluez chaque risque :
    * Probabilité : faible/moyenne/forte
    * Impact : faible/moyen/critique
    * Criticité = probabilité × impact
3. Classez les risques par criticité

**Livrable attendu** : registre des risques avec évaluation

### Notes

* Vous pouvez utiliser les outils de votre choix pour le registre
* Gardez bien le fichier, ça peut toujours servir !
* Prenez le temps de chercher de la documentation sur le sujet

# MON RENDU

Voici mon document qui présente l'analyse des risques liée au projet de modernisation de l'infrastructure (Serveurs, NAS, Firewall, VLAN, Wi-Fi).

## 1. Échelle d'Évaluation
- **Probabilité :** Faible (1), Moyenne (2), Forte (3)
- **Impact :** Faible (1), Moyen (2), Critique (3)
- **Criticité :** Probabilité × Impact

## 2. Tableau des Risques (Classé par Criticité)

| ID | Catégorie | Risque Identifié | Probabilité | Impact | Criticité |
| :--- | :--- | :--- | :---: | :---: | :---: |
| **R01** | Technique | Perte de données lors de la migration (WBS 1.3) | 2 | 3 | **6** |
| **R02** | Humain | Erreur de configuration / Manque de formation alternant (WBS 5.1) | 3 | 2 | **6** |
| **R03** | Technique | Coupure totale internet/réseau lors de la bascule (WBS 3 & 4) | 2 | 3 | **6** |
| **R04** | Technique | Incompatibilité matérielle ou logicielle (OS/AD) (WBS 1.2) | 2 | 2 | **4** |
| **R05** | Organisation | Retard de livraison des équipements (Serveur/Switchs) | 2 | 2 | **4** |
| **R06** | Technique | Mauvaise segmentation VLAN (Accès non autorisés) (WBS 4.1) | 1 | 3 | **3** |
| **R07** | Organisation | Sous-estimation de l'espace de stockage NAS (WBS 2.1) | 2 | 1 | **2** |
| **R08** | Humain | Résistance des utilisateurs aux nouveaux accès Wi-Fi | 2 | 1 | **2** |
| **R09** | Technique | Échec des tests d'intrusion (Vérification sécurité) (WBS 3.3) | 1 | 2 | **2** |
| **R10** | Organisation | Documentation technique obsolète ou incomplète (WBS 5.2) | 1 | 2 | **2** |

---

## 3. Stratégies d'Atténuation (Top 3)

### R01 - Perte de données
* **Action :** Sauvegarde complète (3-2-1) avant migration + Test de restauration.

### R02 - Erreur de l'alternant
* **Action :** Mise en place d'un environnement de pré-production (Lab) + Revue de configuration systématique.

### R03 - Coupure réseau
* **Action :** Réalisation des travaux critiques en heures non-ouvrées + Procédure de "Rollback" prête.