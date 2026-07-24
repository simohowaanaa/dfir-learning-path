# Leçon 2 — Basics of Hard Disks

## Résumé

Comparaison des deux grandes familles de disques (SSD vs HDD) : structure, principes de fonctionnement, et surtout leurs implications radicalement différentes pour la récupération de données en DFIR.

## Points clés

### SSD (Solid State Drive)

- Stocke les données électroniquement sur mémoire flash **NAND**, sans médium magnétique ni pièce mobile.
- Avantages : vitesse, résistance aux chocs, silence, faible consommation.
- Inconvénients : usure des cellules à l'écriture (cycles limités), coût/Go plus élevé.

### HDD (Hard Disk Drive)

- Enregistre les données sur des plateaux rotatifs à revêtement magnétique via des têtes de lecture/écriture mobiles.
- Avantages : grande capacité, meilleur coût/Go.
- Inconvénients : accès plus lent, sensible aux chocs (pièces mobiles).

### Implication DFIR majeure : SSD et HDD ne se comportent pas pareil face à la suppression

- **SSD — commande TRIM** : à la suppression d'un fichier, TRIM indique à l'OS de libérer immédiatement le bloc flash correspondant → les données supprimées deviennent **quasi irrécupérables** rapidement.
- **SSD — wear leveling** : répartit les écritures uniformément sur les cellules physiques pour prolonger la durée de vie du SSD → complique encore la récupération car les données d'un fichier sont dispersées de façon imprévisible.
- **HDD — suppression** : seule la référence dans le système de fichiers est retirée, les données restent physiquement présentes tant qu'elles ne sont pas écrasées → **récupération beaucoup plus fiable**.

### Outils de récupération mentionnés

| Type de disque | Logiciels | Matériel |
|---|---|---|
| HDD | TestDisk, Recuva, R-Studio, EaseUS Data Recovery Wizard | DeepSpar Disk Imager, salle blanche, outils micro-chirurgicaux |
| SSD | Stellar Data Recovery, Ontrack EasyRecovery | Lecteurs NAND, extracteurs de puces mémoire, kits de réparation électronique |

**À retenir** : contre-intuitivement, le SSD (plus moderne/rapide) est le pire cas pour la récupération de preuves, tandis que le HDD (plus ancien/mécanique) est le meilleur allié du DFIR.

## Questions / Réponses

**1. What type of disk has no moving parts and stores data digitally?**
→ **SSD** — stocke les données électroniquement via mémoire flash NAND, aucune pièce mobile.

**2. Which disk is better for data recovery?**
→ **HDD** — le texte conclut explicitement que les disques mécaniques sont plus adaptés à la récupération de données et aux investigations forensiques, contrairement au SSD où TRIM rend la récupération quasi impossible.

**3. What command allows new data to be quickly written over deleted data on SSDs?**
→ **TRIM**

**4. What process writes data to memory cells evenly and extends SSD lifespan?**
→ **Wear Leveling**
