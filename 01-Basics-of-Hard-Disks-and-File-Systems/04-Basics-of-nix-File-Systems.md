# Leçon 4 — Basics of \*nix File Systems

## Résumé

Introduction aux systèmes de fichiers Unix/Linux, avec un focus sur le concept de **journaling**, puis présentation de la famille **EXT** (EXT2/EXT3/EXT4), **ReiserFS**, **Btrfs** et **ZFS**.

## Points clés

### Journaling

- Enregistre les changements du système de fichiers dans un **journal (log)** stocké dans une zone séparée du disque, avant de les appliquer.
- En cas de crash, le système consulte le journal au redémarrage pour identifier les transactions incomplètes et revenir au dernier état stable.
- 3 bénéfices : intégrité/fiabilité des données, récupération rapide après crash, réduction du risque de perte de données.
- Concept transversal déjà rencontré avec NTFS (leçon 3).

### Famille EXT

| Version | Journaling | Taille max fichier/partition | Points clés |
|---|---|---|---|
| EXT2 | Non | 2 To | Premier système EXT, fiable mais basique |
| EXT3 | Oui | 16 To | Ajoute le journaling, rétrocompatible avec EXT2 |
| EXT4 | Oui | 16 To | Allocation différée, meilleures performances, système de fichiers par défaut des distributions Linux modernes |

### ReiserFS

- Sorti en 2001, efficace pour petits fichiers et grands volumes de fichiers.
- Perte de popularité (problèmes juridiques du développeur, développement ralenti) → remplacé majoritairement par EXT4.

### Btrfs (B-Tree File System)

- **Copy-on-Write (CoW)** : toute modification crée d'abord une copie à un nouvel emplacement avant d'écraser l'original → renforce l'intégrité, simplifie les snapshots.
- **Structure B-Tree** pour les métadonnées → performant à grande échelle.
- Snapshots, clonage, checksums (données + métadonnées), allocation dynamique d'inodes, support multi-disques (RAID natif).
- Cas d'usage : serveurs, SAN, NAS, cloud storage.

### ZFS (Z File System)

- Combine système de fichiers et gestionnaire de volumes logiques.
- **Pooled storage**, Copy-on-Write, **checksums + self-healing** (auto-correction des erreurs détectées), snapshots/clonage, **dynamic striping**, **RAID-Z** (évite le "write hole" des RAID classiques), compression et déduplication.
- Cas d'usage : datacenters, cloud storage, sauvegarde/archivage, calcul scientifique.

### Importance DFIR

Les snapshots (Btrfs, ZFS) permettent de reconstituer l'état d'un système à un instant précis — utile en investigation, comparable aux Volume Shadow Copies Windows.

## Questions / Réponses

**1. What feature is implemented in modern file systems to maintain file system integrity and minimize data loss?**
→ **Journaling** — "This process preserves the integrity of the file system and minimizes data loss."

**2. How many times greater is the maximum file size in EXT4 than the maximum file size in EXT2?**
→ **8 fois** (EXT2 = 2 To, EXT4 = 16 To → 16 ÷ 2 = 8).
