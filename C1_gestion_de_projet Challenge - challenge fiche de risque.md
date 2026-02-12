# Plan de Continuité et de Reprise d'Activité (PCA/PRA) - Campus IT

**Document de référence :** Stratégie de résilience post-modernisation.
**Périmètre :** Infrastructure virtualisée (Proxmox), Stockage (TrueNAS), Réseau (pfSense/Aruba).

---

## 1. Scénario d'incident majeur : Rupture d'infrastructure hôte
* **Nature de l'incident :** Panne matérielle critique sur l'hôte de virtualisation principal (**Proxmox VE**).
* **Impact métier :** Interruption de l'Active Directory, du service DNS et du serveur de fichiers partagé.
* **Conséquences :** Indisponibilité immédiate de l'authentification réseau et des ressources pédagogiques pour les 500 usagers du campus.

---

## 2. Dispositif de réponse et de reprise

### A. Mesures de prévention et de détection
* **Politique de sauvegarde (Règle 3-2-1) :** Sauvegardes journalières via **Veeam Backup & Replication** vers une cible **TrueNAS** isolée physiquement.
* **Surveillance proactive :** Supervision via **Zabbix** avec seuils d'alertes sur les indicateurs de santé matérielle (température, SMART des disques, charge CPU).
* **Protection électrique :** Onduleur (UPS) géré par le service **NUT** (Network UPS Tools) pour assurer un arrêt sécurisé des VMs en cas de coupure prolongée.

### B. Procédure de rétablissement (Plan de Reprise)
1. **Initialisation :** Diagnostic de la panne et déclaration de l'incident majeur auprès de la direction.
2. **Priorisation :** Restauration immédiate du **Contrôleur de Domaine (AD)** via la fonction *Instant VM Recovery* de Veeam pour rétablir les accès Wi-Fi et les sessions.
3. **Restauration secondaire :** Remontage du serveur de fichiers et vérification de l'intégrité des partages réseau.
4. **Validation réseau :** Audit rapide des tables de routage sur le firewall **pfSense** et de la segmentation **VLAN** sur les switchs Aruba.

### C. Objectifs de service (SLA)
* **RTO (Recovery Time Objective) :** Temps de rétablissement cible de **4 heures** pour les services critiques.
* **RPO (Recovery Point Objective) :** Perte de données maximale de **24 heures** (basée sur la sauvegarde de la veille).

---

## 3. Indicateurs de performance et de succès (KPI)
* **Taux de disponibilité :** Validation du retour en ligne des services AD et DNS.
* **Intégrité applicative :** Tests de cohérence sur les bases de données et les droits d'accès fichiers.
* **Qualité de service :** Absence d'incidents résiduels lors de la reconnexion simultanée des apprenants.

---

## 4. Matrice de responsabilité du PRA

| Phase | Action Technique | Responsable | Outil |
| :--- | :--- | :--- | :--- |
| **Détection** | Analyse des alertes et logs critiques | Alternant IT | Zabbix / Grafana |
| **Bascule** | Restauration des VMs sur hôte de secours | Responsable IT | Veeam / Proxmox |
| **Réseau** | Vérification de la propagation des VLANs | Responsable IT | pfSense / Aruba |
| **Contrôle** | Tests de recette (connexion utilisateur test) | Alternant IT | Poste Client |