# Challenge E04 : Plan de Reprise d'Activité (mini-PRA)

Ce document formalise la stratégie de continuité et de reprise d'activité suite à la modernisation de l'infrastructure du campus.

---

## 1. Scénario d'incident majeur : Panne Totale du Serveur Principal
* **Nature de l'incident :** Défaillance matérielle critique (ex: carte mère ou contrôleur RAID) de l'hôte de virtualisation **Proxmox VE**.
* **Services impactés :** Active Directory (authentification), Serveur de fichiers, DNS interne et base de données des apprenants.
* **Conséquences :** Arrêt complet des activités pédagogiques et administratives pour les 500 usagers du campus.

---

## 2. Description du Plan de Reprise

### Mesures préventives (Avant l'incident)
* **Sauvegardes (Stratégie 3-2-1) :** Backups journaliers via **Veeam Backup & Replication** vers un **NAS TrueNAS** physiquement séparé.
* **Supervision proactive :** Alertes critiques envoyées par **Zabbix** en cas de dégradation de la santé matérielle (température, erreurs SMART sur les disques).
* **Protection électrique :** Onduleur (UPS) raccordé au service **NUT** pour assurer un arrêt propre des systèmes avant épuisement des batteries.

### Procédures de reprise (Pendant l'incident)
1. **Diagnostic et Alerte :** Confirmation de la panne matérielle et notification de la direction du campus.
2. **Activation du matériel de secours :** Branchement de l'hôte de secours (Cold Standby) ou réutilisation du stockage NAS pour monter les services.
3. **Restauration prioritaire :** Utilisation de la fonction *Instant VM Recovery* de Veeam pour redémarrer le Contrôleur de Domaine (AD) en moins de 30 minutes.
4. **Bascule Réseau :** Vérification de la configuration des VLANs sur les switchs Aruba et du firewall **pfSense** pour rétablir la connectivité Wi-Fi.

### Responsable et Délais de restauration
* **Responsable :** Responsable IT (chef de projet) assisté par l'alternant.
* **RTO (Recovery Time Objective) :** **4 heures** pour le rétablissement de l'accès aux services critiques.
* **RPO (Recovery Point Objective) :** **24 heures** (données de la sauvegarde de la veille à 23h00).

---

## 3. Indicateurs de succès (KPI)
* **Disponibilité :** Rétablissement de l'authentification réseau (AD/DNS) dans les délais impartis.
* **Intégrité :** Absence de perte de données supérieure à 24h et intégrité des fichiers sur le NAS TrueNAS.
* **Qualité de service :** Reprise effective des cours en présentiel sans dysfonctionnement majeur lors de la reconnexion des 500 usagers.