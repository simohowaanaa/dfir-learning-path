# Leçon 4 — Live Data Acquisition Tools

## Résumé

Présentation de l'écosystème d'outils utilisés pour la Live Data Acquisition : suite **Microsoft Sysinternals**, puis en détail **WinPmem**, **FTK Imager**, et **Volatility**.

## Points clés

### Microsoft Sysinternals Tools

Suite d'utilitaires gratuits de Microsoft pour la gestion/dépannage avancé de Windows. Outils les plus pertinents pour le DFIR :

| Outil | Usage |
|---|---|
| AutoRuns / Autorunsc | Liste les programmes/services qui démarrent automatiquement — détecte la persistance de malware |
| Handle | Liste les handles ouverts d'un processus |
| ListDLLs | Liste les DLL chargées par un processus |
| Sysmon | Surveille l'activité système et journalise des événements précis |
| ProcDump | Exporte le dump d'un processus spécifique |
| PsTools | Ensemble d'outils CLI pour gérer les processus à distance |
| RegShot | Instantané du registre pour détecter les changements |
| Strings | Recherche de chaînes de texte dans un fichier/dump mémoire (mots de passe, infos sensibles) |
| LiveKd | Débogueur noyau (kernel debugger) |

### WinPmem

Outil de dump mémoire léger, sans installation. Commande (PowerShell/CMD en admin) :
```
Winpmem_mini_x64_rc2.exe memdump.raw
```
Produit un fichier `.raw` analysable ensuite avec un outil comme Volatility.

### FTK Imager

Outil pour imager disques ET mémoire sur Windows. Procédure de capture mémoire :
1. Lancer en tant qu'administrateur
2. Menu `File > Capture Memory...`
3. Choisir le chemin de destination
4. Cliquer sur **Capture Memory**
5. Résultat : fichier `memdump.mem`

Outil de référence pour la capture mémoire en réponse à incident.

### Volatility

Outil de référence pour l'**analyse** (pas la capture) des images mémoire, Linux et Windows, écrit en Python.

- Installation : télécharger Volatility3 (GitHub), installer Microsoft C++ Build Tools, le package Python `snappy` (version spécifique), puis `pip install -r requirements.txt`.
- Utilisation : `python .\vol.py -f memdump.mem windows.info.Info`
  - `-f` : fichier image mémoire à analyser
  - `windows.info.Info` : plugin Volatility utilisé (ici infos système générales : kernel base, NTBuildLab, SystemTime...)

### Flux de travail typique

1. **Capturer** la RAM avec FTK Imager ou WinPmem → fichier `.mem`/`.raw`
2. **Analyser** ce fichier avec Volatility (plugins selon l'objectif : processus, connexions réseau, DLL chargées...)
3. Utiliser les outils Sysinternals en complément pour des vérifications ciblées en direct

## Questions / Réponses

**1. What is the name of the memory analysis tool developed in Python that is used to analyze both Linux and Windows memory images?**
→ **Volatility** — "Volatility is a powerful tool for analyzing both Linux and Windows memory images. Developed in Python..."

**2. What is the name of the Sysinternals tool that lists and manages programs and services that start automatically at system startup?**
→ **AutoRuns** — "AutoRuns : Lists and manages programs and services that start automatically at system startup."
