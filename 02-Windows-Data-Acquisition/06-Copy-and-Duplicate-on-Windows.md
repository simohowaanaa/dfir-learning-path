# Leçon 6 — Copy and Duplicate on Windows

## Résumé

Dernière leçon de la section : pourquoi on travaille toujours sur des copies en DFIR, les méthodes d'acquisition (bit-level vs sélective), les formats d'image disque, et la procédure de création d'image avec FTK Imager.

## Points clés

### Intégrité des données

- On n'analyse jamais l'original — toute action sur les données originales peut compromettre leur intégrité.
- Importance : évite les fausses conclusions, permet la **répétabilité** (différents experts doivent arriver aux mêmes conclusions).
- Facteurs de risque : pannes matérielles, bugs, altération intentionnelle, modifications accidentelles.
- Mesures de protection : backups, valeurs de hash, write protection, outils forensiques dédiés.
- Dimension légale : réglementations sur la collecte/stockage/analyse des preuves numériques.

### Méthodes d'acquisition

- **Bit-Level Copy** : copie exacte bit par bit (disque physique/logique), y compris données supprimées/corrompues/cachées. Variantes : Sector Copy, File Copy, Memory Copy.
  - Avantages : copie exacte, fiable (détection d'erreurs).
  - Inconvénients : complexe (outils/matériel spécialisés), lent sur gros volumes.
- **Selective Copy** : copie de fichiers/dossiers spécifiques uniquement.

### Formats d'image disque

| Format | Caractéristiques |
|---|---|
| Raw (dd) | Copie exacte bit à bit, aucune métadonnée/structure. Extensions `.img`/`.bin`. Compatibilité maximale. |
| SMART | Format forensique avec métadonnées et logs pour tracer les opérations. |
| E01 | Développé par EnCase. Compressé, hash intégrés, mot de passe optionnel. |
| AFF (Advanced Forensic Format) | Open-source, compresse/segmente, vérifie l'intégrité par hash cryptographiques, métadonnées sur les opérations, supporte le **chiffrement**. |

### Procédure de création d'image (FTK Imager)

1. Sélectionner la partition/disque → clic droit → "Create Image"
2. Choisir le type d'image (ex. AFF)
3. Renseigner les infos de cas : Case Number, Evidence Number, Unique Description, Examiner, Notes → chain of custody
4. Choisir dossier de destination et nom du fichier
5. Option "Use AFF Encryption" pour protéger l'image par mot de passe
6. Options : "Verify images after they are created", "Create directory listings of all files"
7. **Start** → génère 3 fichiers : `.aff` (image compressée), `.txt` (log avec hashs MD5/SHA1 et vérification), `.csv` (liste des fichiers de l'image)

### Hash values et signatures numériques

- Vérifient que les données copiées n'ont pas été altérées (hash original == hash copie → intégrité prouvée).
- **CertUtil.exe** (outil Windows natif) : `certutil -hashfile memdump.mem SHA256` — paramètre `-hashfile` pour calculer le hash d'un fichier avec l'algorithme spécifié.

### Cadre légal et éthique

Respecter les lois et politiques de confidentialité, particulièrement pour les données personnelles ; certaines obligations légales exigent des procédures de signature/vérification pour la recevabilité des preuves.

## Questions / Réponses

**1. What is the process of making an exact copy of a disk or partition without checking the file system, metadata, etc.?**
→ **Bit-Level Copy** (copie Raw/dd) — copie chaque bit individuellement, sans dépendre du système de fichiers ou des métadonnées.

**2. What is the name of an open-source file format designed for forensic purposes that supports encryption of images?**
→ **AFF** — "AFF (Advanced Forensic Format) is an open-source file format designed for forensic purposes" et supporte le chiffrement via "Use AFF Encryption".

**3. What is the name of the tool used in Windows to calculate the hash value of a file with the parameter "-hashfile"?**
→ **CertUtil** (CertUtil.exe) — "it must be run with the '-hashfile' parameter."
