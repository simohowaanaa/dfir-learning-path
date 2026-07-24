# Leçon 2 — Volatile and Non-Volatile Data on Windows

## Résumé

Détail concret des deux types de données introduits en leçon 1, avec les outils utilisés pour chacun.

## Points clés

### Volatile Data

- Perdue à la coupure d'alimentation.
- Exemples : contenu de la **RAM**, caches CPU, registres système, informations de connexions réseau.
- Sur un système compromis mais pas encore redémarré, on peut retrouver les traces d'un attaquant via les données volatiles — perdues définitivement après un reboot.
- Règle d'or DFIR : ne jamais éteindre une machine compromise avant d'avoir capturé sa mémoire vive.
- Outils/commandes : **FTK Imager**, **procdump** (copie RAM) ; **netstat** (connexions réseau) ; **tasklist** (processus en cours).

### Non-Volatile Data

- Survit à une coupure d'alimentation. Supports : HDD, SSD, clés USB, CD/DVD.
- Contenu typique : configurations système, fichiers utilisateurs, logs, données d'applications.
- Collecte via copie **bit à bit** (`dd`, duplicateurs forensiques).
- Calcul et enregistrement des **valeurs de hash** (MD5, SHA-256) pour prouver l'authenticité et l'absence de modification — principe de chain of custody.

### Synthèse

| | Volatile Data | Non-Volatile Data |
|---|---|---|
| Persiste après coupure ? | Non | Oui |
| Exemples | RAM, caches CPU, registres, connexions réseau | HDD/SSD, USB, CD/DVD |
| Collecte | Live (FTK Imager, procdump, netstat, tasklist) | Copie bit à bit + hash de vérification |
| Urgence | Très haute — disparaît au reboot | Plus stable dans le temps |

## Questions / Réponses

**1. What type of data is no longer accessible when the power supply of the computer is turned off?**
→ **Volatile Data**

**2. What is the type of data that is stored despite a power supply interruption?**
→ **Non-Volatile Data**
