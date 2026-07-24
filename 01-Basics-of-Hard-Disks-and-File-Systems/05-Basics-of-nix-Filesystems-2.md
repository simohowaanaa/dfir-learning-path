# Leçon 5 — Basics of \*nix Filesystems - 2

## Résumé

Suite de la leçon précédente : **XFS**, **SquashFS**, **tmpfs**, puis synthèse comparative de tous les systèmes de fichiers Linux vus dans la section.

## Points clés

### XFS

- Développé par SGI pour IRIX, porté sur Linux. Conçu pour la très haute performance et l'échelle (jusqu'au pétaoctet).
- **Stockage séparé des métadonnées** → accès plus rapide, surtout sur gros systèmes de fichiers.
- **Journaling ciblé métadonnées uniquement** → protège l'intégrité sans pénaliser la vitesse d'écriture des données.
- **Allocation Groups** : le FS est divisé en sections indépendantes gérables en parallèle.
- **Delayed Allocation** : optimise le placement physique des données.
- **Extent-based Allocation** : fichiers stockés en blocs contigus ("extents") → réduit la fragmentation.
- Cas d'usage : production vidéo, calcul scientifique, big data, serveurs de fichiers, datacenters.

### SquashFS

- Système de fichiers **compressé** et **en lecture seule (read-only)**.
- Supporte plusieurs algorithmes de compression (LZMA, LZO, Gzip, XZ).
- **Immuable** une fois créé → idéal pour systèmes live et embarqués, empêche la modification malveillante.
- **Déduplication par blocs**, **accès aléatoire** aux données compressées.
- Cas d'usage : distributions Linux live, systèmes embarqués, packaging d'applications.

### Tmpfs

- Système de fichiers vivant **en RAM** (ou en swap si besoin) — aucun accès disque.
- Accès extrêmement rapide, taille dynamique ajustable.
- **Non persistant** : données perdues au reboot ou démontage.
- Répertoires typiques : `/tmp`, `/var/tmp`, `/dev/shm`.
- Cas d'usage : fichiers temporaires, cache d'applications, IPC.
- Limite : capacité bornée par la mémoire système disponible.

### Synthèse comparative

| Feature | EXT4 | XFS | ZFS | Btrfs | SquashFS | Tmpfs |
|---|---|---|---|---|---|---|
| Journaling | Oui | Oui | Oui | Oui | Non | Non |
| Taille max fichier | 16 To | 18 Eo | 128 Eo | 16 Eo | 4 Go | — |
| Taille max volume | 16 To | 50 To | 256 To | 16 Eo | — | — |
| Sécurité | Moyenne | Moyenne | Élevée | Élevée | Faible | Faible |
| Performance | Rapide | Rapide | Moyenne | Moyenne | Rapide | Très rapide |
| Usage | HDD/SSD | HDD/SSD | NAS, serveurs | HDD/SSD | Embarqué, Live CD | Disques RAM |

### Point crucial pour le DFIR

Un système Linux en fonctionnement peut utiliser **plusieurs systèmes de fichiers simultanément** (ex : `/` en EXT4, `/tmp` en tmpfs, un volume NAS en ZFS). Avant toute analyse DFIR, il faut d'abord identifier tous les disques/systèmes de fichiers présents et planifier une méthodologie spécifique à chacun.

## Questions / Réponses

**1. Which file system supports large files, has high storage capacity, and features efficient use of metadata and journaling?**
→ **XFS** — "distinguished by its capacity to support large files, high storage capacity, and scalability (...) efficient metadata management and advanced journaling mechanisms."

**2. What is the read-only file system designed as a compressed file system, typically used for live Linux distributions, embedded systems, and application packaging?**
→ **SquashFS** — "SquashFS is designed as a read-only, compressed file system, primarily used for live Linux distributions, embedded systems, and application packaging."

**3. What file system has a file size limit of 128 EB and a partition size limit of 256 TB, commonly used on servers?**
→ **ZFS** — d'après le tableau comparatif (File Size Limit = 128 EB, Volume Size Limit = 256 TB, Application = "NAS, servers").
