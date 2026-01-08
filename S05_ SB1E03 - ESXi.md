# Procédure d'installation de VCenter (VCSA)

## 1. Préparation et Lancement
* **Montage de l'image** : Faire un double-clic sur le fichier ISO de vCenter pour le monter.
* **Accès à l'installeur** : Naviguer dans le répertoire suivant :
    `E:\vcsa-ui-installer\win32`
* **Exécution** : Lancer le fichier `installer.exe`.

![alt text](images/image-96.png)

---

## 2. Étape 1 : Déploiement de l'appareil (Stage 1)

### Introduction et Licence
1. Cliquer sur **Next** sur l'écran d'accueil.
2. Accepter le contrat de licence (EULA) et cliquer sur **Next**.

### Configuration de l'ESXi cible
Indiquez l'hôte sur lequel la VM vCenter sera déployée :
* **IP du serveur ESXi** : `172.16.0.100`
* **Nom d'utilisateur** : `root`
* **Mot de passe** : `XXXX`

*Note : Validez le certificat de sécurité qui s'affiche.*

> **Attention** : Si l'adresse IP s'affiche en rouge, effacez-la et retapez-la manuellement (problème fréquent de caractères invisibles).

![alt text](images/image-97.png)
![alt text](images/image-98.png)

### Paramètres de la VM vCenter
* Définir le **nom de la machine** et le **mot de passe root**.
* Cliquer sur **Next**.

![alt text](images/image-99.png)

### Taille du déploiement
* **Choix** : `Tiny` (C'est l'option la plus basse, elle définit les ressources CPU/RAM allouées).
* Laisser par défaut et cliquer sur **Next**.

![alt text](images/image-100.png)

### Sélection du Datastore
* Sélectionner le datastore où installer la VM.
* **Option Disk Mode** : Cocher **"Enable Thin Disk Mode"** pour ne consommer que l'espace nécessaire (allocation dynamique).

![alt text](images/image-102.png)

* *Info : On peut aussi choisir un stockage de type VSAN pour la mutualisation.*

![alt text](images/image-101.png)

### Configuration du réseau
* Configurer l'adresse IP fixe pour le vCenter.
* **IP dédiée** : `172.16.0.101`
* (Pensez à remplir le masque, la passerelle et le DNS selon votre réseau).

![alt text](images/image-103.png)

### Déploiement du serveur.

![alt text](images/image-104.png)

---

## 3. Fin du Stage 1
Le déploiement de l'appareil est lancé. Une fois la barre de progression terminée, le Stage 1 est validé, noté l'adresse qui est indiqué à la fin du stage 1.

![alt text](images/image-106.png)


## 4. Étape 2 : Configuration de l'appareil (Stage 2)

### Ouverture de la console de la VM VMware Vcenter Server 

![alt text](images/image-108.png)

### Ouverture de la page de la VM VMware Vcenter Server et cliquer sur installation

![alt text](images/image-107.png)

![alt text](images/image-109.png)

### verifier que les paramètres sont corrects : 

![alt text](images/image-110.png)


### configuration du SSO Vcenter : 

* *Info : Le SSO de Vcenter est un SSO intégré avec son propre domaine car les différentes briques "déploiement, stockages, inventaires..." doivent pouvoir s'authentifier entre elles .*

* MEttre le même domaine
* Choisir un mot de passe

### Configurer le CEIP , au choix , si du test, pas besoin : 

![alt text](images/image-111.png)


### verifier que les paramètres sont corrects 

![alt text](images/image-112.png)

### lancer la configuration du stage 2 : 

![alt text](images/image-113.png)

### Fin de configuration du stage 2 : 

![alt text](images/image-114.png)

### Lancement de VSPHERE CLIENT , utiliser les logins du SSO : 

* nom de domain: XXXXX
* login :administrator@NOMDUDOMAIN
* mdp : XXXXXXX

![alt text](images/image-115.png)

### Fin du stage 2  : 

* appliance de management joignable et fonctionnelle

* console d'administration de VCENTER joignable et fonctionnelle

![alt text](images/image-116.png)

--------------------------------------------------

### Création d’un Cluster 

# Procédure : Création d'un Cluster vSphere

## 1. Accéder à l’assistant de création du cluster
1. Dans l’inventaire vSphere, effectuez un **clic droit** sur le **Datacenter**.
2. Sélectionnez **Nouveau cluster…**
3. L’interface de paramétrage du cluster apparaît.

![alt text](images/image-117.png)

---

## 2. Paramétrer les options du cluster
À ce stade, nous **n’activons pas** les options suivantes (elles seront configurées ultérieurement) :

* **vSphere DRS (Distributed Resource Scheduler) :** Permet de répartir automatiquement la charge de travail entre les hôtes du cluster afin d’optimiser les performances et l’utilisation des ressources.
* **vSphere HA (High Availability) :** Assure la haute disponibilité en redémarrant automatiquement les machines virtuelles sur un autre hôte en cas de défaillance d’un serveur ESXi.
* **vSAN (Virtual Storage Area Network) :** Combine automatiquement les disques locaux de chaque hôte ESXi pour créer un seul datastore partagé.

![alt text](images/image-118.png)

### Étapes de configuration :
1. Renseigner le **nom du cluster**.
2. Cocher **Créer une image**.
3. Choisir **Gérer la configuration au niveau du cluster** :
    > **Note sur l'impact :** Cette option applique la configuration logicielle (ESXi, drivers, firmware) à l’ensemble des hôtes du cluster. Toute erreur de configuration sera répliquée sur tous les nœuds.
4. Cliquer sur **Suivant**.

![alt text](images/image-119.png)

* Cliquer sur **Suivant**.

## 4. Compte rendu
Un récapitulatif apparaît :
1. Vérifier les paramètres.
2. Valider pour finaliser la configuration.

![alt text](images/image-120.png)

> **Résultat :** Le cluster est maintenant créé et visualisable dans l’interface.

---

## 5. Ajouter les nœuds au cluster créé
1. Depuis l’inventaire, **glisser-déposer** les hôtes ESXi dans le cluster.
2. Les hôtes héritent automatiquement de la configuration définie au niveau du cluster.

![alt text](images/image-121.png)

![alt text](images/image-122.png)