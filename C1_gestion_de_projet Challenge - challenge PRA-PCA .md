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

# Procédure Technique d'Urgence : Exécution du PRA

**Cible :** Alternant IT  
**Objectif :** Rétablir les services critiques en moins de 4 heures suite à une panne du serveur Proxmox.

---

## Étape 1 : Diagnostic et Isolation (0 - 30 min)
* [ ] **Vérifier l'état physique :** Confirmer la panne matérielle (voyants orange/rouge, absence de réponse ping sur l'IP de management).
* [ ] **Couper l'alimentation :** Débrancher le serveur défectueux pour éviter tout conflit d'IP si celui-ci redémarre par intermittence.
* [ ] **Alerter le responsable :** Confirmer le basculement officiel en mode PRA.

## Étape 2 : Restauration des Services Critiques (30 min - 2h)
* [ ] **Ouvrir la console Veeam :** Se connecter à l'instance Veeam Backup & Replication.
* [ ] **Instant VM Recovery (Priorité 1) :** Sélectionner la VM **Contrôleur de Domaine (AD/DNS)**.
    * Choisir le point de restauration de la veille (23h00).
    * Monter la VM sur l'hôte de secours ou directement depuis le stockage TrueNAS.
* [ ] **Démarrage et Test AD :** Une fois la VM lancée, vérifier que les services DNS répondent correctement via un `nslookup`.

## Étape 3 : Restauration des Données Utilisateurs (2h - 3h)
* [ ] **Instant VM Recovery (Priorité 2) :** Lancer la restauration du **Serveur de Fichiers**.
* [ ] **Vérification TrueNAS :** S'assurer que les partages réseaux (SMB/NFS) sont accessibles depuis un poste de test.
* [ ] **Contrôle des Quotas :** Vérifier que les limites de stockage par utilisateur sont toujours actives.

## Étape 4 : Vérification Réseau et Wi-Fi (3h - 3h30)
* [ ] **Console pfSense :** Vérifier que le portail captif et le serveur DHCP distribuent les adresses aux usagers.
* [ ] **Dashboard UniFi :** Confirmer que les bornes Wi-Fi sont bien connectées au nouveau contrôleur.
* [ ] **Test VLAN :** Vérifier l'isolation entre le VLAN "Étudiants" et le VLAN "Administration".

## Étape 5 : Clôture et Communication (3h30 - 4h)
* [ ] **Recette utilisateur :** Se connecter avec un compte test "Apprenant" pour valider l'ouverture de session et l'accès internet.
* [ ] **Rapport d'incident :** Noter l'heure de rétablissement et les éventuels incidents rencontrés durant la procédure.
* [ ] **Information générale :** Notifier la direction que les services sont à nouveau opérationnels.