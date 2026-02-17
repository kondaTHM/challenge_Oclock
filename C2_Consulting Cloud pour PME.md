# Recommandation Stratégique Cloud : MediCare+

**Client :** MediCare+ (PME Santé)  
**Consultant :** TechConseil  
**Objectif :** Modernisation, Sécurité (RGPD) et Réduction des Coûts.

---

## 1. Architecture Cible

L'objectif est de passer d'une gestion matérielle lourde à une gestion de services (PaaS/SaaS) afin de décharger l'administrateur système et d'assurer une haute disponibilité.

| Composant | Proposition | Modèle | Provider | Justification courte |
| :--- | :--- | :--- | :--- | :--- |
| **Identités** | Microsoft Entra ID | SaaS | Microsoft | Centralise l'accès et sécurise le télétravail (MFA). |
| **Bureautique** | Microsoft 365 Business | SaaS | Microsoft | Standard du marché, inclut Teams pour la collaboration. |
| **Fichiers** | SharePoint / OneDrive | SaaS | Microsoft | Remplace le NAS. Accès sécurisé partout sans VPN. |
| **App métier** | Web App (PHP) | PaaS | Azure | Plus de serveur à gérer. Scalabilité simplifiée. |
| **Base de données** | Azure DB for MySQL | PaaS | Azure | Sauvegardes auto et haute disponibilité native. |
| **Sauvegardes** | Azure Backup | PaaS | Azure | Automatisation totale des données critiques. |
| **Site web** | Hébergement managé | PaaS | OVHcloud | Faible coût, isolation de l'application métier. |



---

## 2. Choix du Provider

Comparaison des solutions envisagées pour le cœur de l'infrastructure :

| Critère | Azure (Microsoft) | AWS (Amazon) | OVHcloud |
| :--- | :--- | :--- | :--- |
| **Localisation France** | Oui (Paris/Marseille) | Oui (Paris) | Oui (Plusieurs sites) |
| **Services PaaS** | Très complets & intégrés | Exhaustifs (complexes) | Limités mais simples |
| **Coût estimé** | Moyen (optimisé M365) | Moyen / Élevé | Faible |
| **Support / Simplicité** | Idéal pour env. Windows | Courbe d'apprentissage | Support parfois lent |

**Décision :** Le fournisseur retenu est **Azure (Microsoft)**.  
C'est le choix de la cohérence : MediCare+ utilise déjà l'écosystème Windows. L'intégration native entre la bureautique (M365) et l'infrastructure cloud réduit la complexité technique et facilite la mise en conformité **RGPD** via des serveurs localisés en France.

---

## 3. Estimation Budgétaire (Ordre de grandeur)

L'estimation repose sur une consommation standard pour 50 utilisateurs :

* **Licences Microsoft 365 Business Premium :** ~1 000 € / mois (sécurité incluse).
* **Hébergement Azure (App + MySQL + Stockage) :** ~400 € / mois.
* **Hébergement Site Web (OVH) :** ~20 € / mois.

**Total mensuel estimé : ~1 420 €** (soit environ **17 000 € / an**).  
*Note : Cela représente une économie de plus de 60% par rapport aux 46 000 € actuels, tout en modernisant l'outil de travail.*

---

## 4. Points d'attention et Risques

1.  **Migration des données :** Le transfert des fichiers du NAS vers le Cloud peut être long.
    * *Solution :* Utilisation de l'outil *Migration Manager* et déploiement progressif par agence.
2.  **Accompagnement au changement :** L'équipe est peu familière avec ces outils.
    * *Solution :* Formation courte sur Teams/SharePoint et documentation des nouvelles procédures de télétravail.
3.  **Dépendance fournisseur (Lock-in) :** Risque lié à l'écosystème unique Microsoft.
    * *Solution :* Le site web reste chez OVHcloud pour maintenir une indépendance externe.
4.  **Sécurité & RGPD :** Risque de fuite de données sur le cloud.
    * *Solution :* Activation systématique de l'authentification multi-facteurs (MFA) et chiffrement des données au repos.

---

