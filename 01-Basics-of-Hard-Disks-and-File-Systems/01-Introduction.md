# Leçon 1 — Introduction

## Résumé

Leçon de mise en contexte : pourquoi le DFIR (Digital Forensics and Incident Response) existe, et pourquoi les disques et systèmes de fichiers en sont le cœur.

## Points clés

- **DFIR = Digital Forensics + Incident Response**
  - *Digital Forensics* : collecte, examen et préservation des preuves numériques (enquête).
  - *Incident Response* : détection, isolement (containment) et remédiation rapide d'un incident (réaction).
- Un spécialiste DFIR détermine l'ampleur des dégâts, la source de l'attaque, l'identité de l'attaquant, et propose des mesures préventives.
- **Une grande partie des preuves est stockée sur les disques** — chaque action (fichier, utilisateur, système) y laisse une trace.
- Concept fondamental (fil rouge de tout le cours) : **supprimer un fichier ≠ effacer ses données**. En général, seul le pointeur/la référence dans le système de fichiers est retiré, pas le contenu lui-même.

### 6 raisons pour lesquelles disques et systèmes de fichiers sont critiques en DFIR

1. Stockage et organisation des données
2. Récupération de données supprimées (via les métadonnées du système de fichiers)
3. Timestamps et activité utilisateur (reconstitution de chronologie)
4. Analyse de données cachées/chiffrées
5. Logs système et artefacts OS (stockés eux-mêmes dans le système de fichiers)
6. Compatibilité cross-plateforme (NTFS, ext4, APFS, etc.)

## Questions / Quiz

Aucune question associée à cette leçon (*No Answer Needed*).
