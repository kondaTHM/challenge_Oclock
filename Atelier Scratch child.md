

## Étape 1 : Créer les Variables (Catégorie Orange)
Avant de coder, crée les 4 "boîtes" dont le Chat a besoin :
1. Va dans **Variables** (Orange).
2. Clique sur **Créer une variable**.
3. Crée ces 4 variables : `Nombre Mystère`, `Essai`, `Tentatives`, et `Record`.

## Étape 2 : Préparer le début du jeu
On installe les règles quand on clique sur le drapeau vert.
1. Prends le bloc `Quand le drapeau vert est cliqué` (**Jaune**).
2. Accroche en dessous les blocs suivants (**Orange**) :
    * `Mettre [Nombre Mystère] à (nombre aléatoire entre 1 et 100)` -> *Le bloc arrondi "nombre aléatoire" est chez les **Verts**.*
    * `Mettre [Tentatives] à 0`.
    * `Mettre [Essai] à 0`.

## Étape 3 : Faire deviner le nombre
On veut que le Chat demande le nombre tant que tu n'as pas trouvé.
1. Prends le bloc `Répéter jusqu'à ce que < ... = ... >` (**Orange foncé**).
2. Dans le trou hexagonal, mets l'opérateur `=` (**Vert**).
3. Dans les deux ronds de l'opérateur, glisse la variable `(Essai)` (**Orange**) et la variable `(Nombre Mystère)` (**Orange**).
4. **À l'intérieur de la boucle**, ajoute :
    * `Demander [Propose un nombre entre 1 et 100 !] et attendre` (**Bleu clair**).
    * `Mettre [Essai] à (réponse)` -> *La bulle bleue `(réponse)` est juste en dessous du bloc demander.*
    * `Ajouter 1 à [Tentatives]` (**Orange**).

## Étape 4 : Donner les indices (Plus ou Moins)
Toujours **DANS la boucle**, sous les blocs précédents, aide le joueur avec ces conditions :
1. Prends un bloc `Si < ... < ... > alors` (**Orange foncé**) :
    * Si `< (Essai) < (Nombre Mystère) >` (**Vert**) : alors `Dire [C'est PLUS !] pendant 1 seconde`.
2. Prends un bloc `Si < ... > ... > alors` (**Orange foncé**) :
    * Si `< (Essai) > (Nombre Mystère) >` (**Vert**) : alors `Dire [C'est MOINS !] pendant 1 seconde`.

## Étape 5 : Gagner et enregistrer le Record
**SOUS la grande boucle** (quand l'essai est enfin égal au nombre mystère) :
1. `Dire (Regrouper [Bravo ! Trouvé en ] et (Tentatives))` pendant 3 secondes.
    * *Astuce : Le bloc `regrouper` est **Vert**. Glisse la variable `(Tentatives)` dans le deuxième mot.*
2. Pour le record, ajoute ce bloc :
   * `Si << (Tentatives) < (Record) >> ou << (Record) = 0 >> alors` (**Orange foncé** + **Vert**) :
     * `Mettre [Record] à (Tentatives)`
     * `Dire [NOUVEAU RECORD !] pendant 2 secondes.

## Atelier : Bonus (Pour les Pros !)

Si ton jeu fonctionne, essaie d'ajouter ces fonctions. **C'est du bonus, cherche bien !** 😈
