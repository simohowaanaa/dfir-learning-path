# Leçon 3 — Windows File System Fundamentals

## Résumé

Présentation des 3 systèmes de fichiers Windows — **FAT32**, **NTFS**, **exFAT** — leur structure, leurs principes de fonctionnement, et leur importance pour le DFIR.

## Points clés

### FAT32 (File Allocation Table 32)

- Introduit en 1996 (Windows 95 OSR2), simple et très compatible.
- **FAT (File Allocation Table)** : table centrale qui indique où sont situés les fragments (clusters) de chaque fichier sur le disque, permettant de les réassembler dans le bon ordre.
- **Root Directory** : dynamique en taille et emplacement (contrairement à FAT16).
- Suppression : les clusters sont juste marqués "libres" dans la FAT, le contenu réel n'est pas effacé → bon pour la récupération forensique.
- Limites : fichier max **4 Go**, partition max ~8 To en théorie (souvent moins en pratique), pas de sécurité avancée.

### NTFS (New Technology File System)

- Système de fichiers moderne de Windows, riche en métadonnées.
- **MFT (Master File Table)** : contient une entrée pour **chaque fichier et dossier**, avec toutes ses métadonnées (nom, dates, permissions, emplacement physique). Chaque entrée MFT est composée d'attributs (`$FILE_NAME`, `$DATA`, `$STANDARD_INFORMATION`, `$SECURITY_DESCRIPTOR`, etc.).
- **Journaling** : enregistre les changements du système de fichiers pour permettre une restauration après crash — précieux aussi comme preuve forensique.
- **Sécurité/permissions** : DACL, SACL, propriétaire/groupe via `$SECURITY_DESCRIPTOR`.
- Supporte compression et chiffrement natifs (+ BitLocker en option).
- Avantages : gros fichiers/partitions, sécurité avancée, intégrité des données.
- Inconvénients : structure plus complexe, incompatibilité possible avec anciens systèmes, plus gourmand en ressources.

### exFAT (Extended FAT)

- Conçu par Microsoft pour les supports amovibles (clés USB, cartes SD), pour dépasser les limites de FAT32 sans la complexité de NTFS.
- Utilise une FAT étendue + **adressage 64 bits** (jusqu'à 16 exbibytes théoriques pour fichiers/partitions).
- Suppression : même logique que FAT32 — clusters libérés mais contenu non effacé physiquement, récupérable.
- Avantages : plus de limite à 4 Go, large compatibilité.
- Inconvénient : pas de fonctionnalités de sécurité avancées comme NTFS.

### Tableau comparatif

| Critère | FAT32 | exFAT | NTFS |
|---|---|---|---|
| Taille max fichier | 4 Go | 16 Eo | 16 Eo |
| Taille max partition | 2 To | 16 Eo | 256 To |
| Noms de fichiers | 8.3 caractères (limité) | 255 (Unicode) | 255 (Unicode) |
| Sécurité | Faible | Faible | Élevée (permissions, chiffrement) |
| Usage typique | Clés USB, vieux appareils | Disques externes, SSD externes | Disques internes, NAS |

### Importance DFIR

- NTFS (MFT, permissions, journaling) offre les métadonnées les plus riches pour reconstituer accès/modifications.
- FAT32/exFAT : structures plus simples, l'analyse forensique se concentre sur la récupération de fichiers supprimés et l'examen des timestamps.

## Questions / Réponses

**1. What is the name of the NTFS file system structure that contains an entry for every file and folder?**
→ **MFT** (Master File Table) — "the MFT, which contains a record for every file and folder in the file system."

**2. What FAT32 file system structure holds location information for each file or folder?**
→ **FAT** (File Allocation Table) — "The FAT is the core of FAT32 (...) indicating the location of the file on the drive."

**3. How many bits does exFAT use for addressing?**
→ **64 bits** — "exFAT uses 64-bit addressing to determine the locations of files and folders on the disk."

**4. What is the file size limit in GB for FAT32?**
→ **4 GB** — "Maximum file size limit of 4GB."
