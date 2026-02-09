### CHALLENGE 1 : Gestion de projet LA NOTE DE CADRAGE DU BESOIN

# challenges C01

Ces challenges sont un projet fil rouge a suivre toute la saison C01

## Énoncé E1

### Contexte

Vous êtes responsable de l'informatique au sein d'un campus de formation professionnelle (en présentiel 😁).

Le campus compte en permanence environ 500 personnes, entre les salariés (une quinzaine), les formateurs (freelances, formateurs occasionnels) et les apprenants (formation continue et alternance).

La direction vous demande de moderniser l’infrastructure IT du campus pour accueillir de nouveaux services numériques : serveurs fichiers, NAS, firewall, VLAN et accès sécurisé Wi-Fi.

Dans votre service, vous accueillez actuellement un alternant.

---
## 📄 Fiche de Cadrage du Projet

### 1. Objectifs du projet
L'objectif est de mettre à jour l'infrastructure réseau et de stockage pour répondre aux besoins de croissance et de sécurité du campus.
* **Modernisation du stockage :** Mise en place d'un serveur de fichiers/NAS pour centraliser les données.
* **Sécurisation réseau :** Déploiement d'un Firewall et segmentation du trafic via des VLANs (Isoler l'administration des apprenants).
* **Mobilité sécurisée :** Déploiement d'une solution Wi-Fi avec authentification sécurisée pour 500 utilisateurs simultanés.

### 2. Périmètre et exclusions
* **Périmètre :**
    * Audit de l'infrastructure réseau existante.
    * Installation et configuration du matériel (Switchs, Firewall, Bornes Wi-Fi, NAS).
    * Paramétrage des droits d'accès et des politiques de sécurité.
    * Formation de l'alternant sur les nouvelles technos déployées.
* **Exclusions :**
    * Maintenance des postes de travail individuels des apprenants (BYOD).
    * Développement d'applications métiers spécifiques.
    * Travaux de câblage lourd (génie civil).

### 3. Parties prenantes
| Catégorie | Acteurs |
| :--- | :--- |
| **Interne** | Direction du campus, Responsable IT (Chef de projet), Alternant, Personnel administratif, Formateurs internes, Apprenants. |
| **Externe** | Prestataires réseaux/Cloud, Fournisseurs de matériel informatique, Formateurs freelances, Opérateur Fibre/Internet. |

### 4. Livrables principaux
* **Audit de l'existant :** État des lieux technique.
* **Schéma réseau cible :** Plan d'adressage IP et architecture des VLANs.
* **Infrastructure opérationnelle :** Firewall configuré, Wi-Fi actif, NAS accessible.
* **Documentation technique :** Procédures d'exploitation et de secours (PRA/PCA).
* **Guide de connexion :** Document simplifié pour les utilisateurs (Wi-Fi et partage de fichiers).

### 5. Contraintes Qualité / Coût / Délai
* **Qualité :** Haute disponibilité du service Wi-Fi (QoS pour les cours en ligne) et étanchéité stricte entre les réseaux (VLAN).
* **Coût :** Budget défini par la direction pour l'acquisition du matériel (Hardware) et les licences logicielles.
* **Délai :** Déploiement complet attendu pour la prochaine période de rentrée scolaire (Session C01).