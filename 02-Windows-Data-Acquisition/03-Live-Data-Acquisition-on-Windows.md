# Leçon 3 — Live Data Acquisition on Windows

## Résumé

Mise en pratique de la collecte de données volatiles/non-volatiles pendant que le système est encore en fonctionnement, en minimisant les modifications apportées.

## Points clés

### Pourquoi c'est indispensable

- Préserve les données volatiles qui disparaîtraient à l'arrêt du système.
- Permet de continuer à faire fonctionner des systèmes critiques qui ne peuvent pas être arrêtés.
- Minimise les altérations du système → renforce l'intégrité des preuves → augmente leur recevabilité en justice.

### 1. Contenu de la RAM

| Méthode | Description | Avantage | Inconvénient |
|---|---|---|---|
| Hardware | Lecture directe des puces mémoire via matériel spécialisé | Résultat le plus fiable | Coûteux, nécessite matériel/expertise spécifiques, rarement nécessaire |
| Software | Un programme dans l'OS génère un dump mémoire | Plus simple | Pas toujours garanti d'être une copie exacte (dépend config OS/outils de sécurité) |

### 2. Trafic réseau

Surveiller/enregistrer connexions actives et trafic réseau → comprendre point de départ d'un incident, sa progression, une éventuelle exfiltration de données ou un acteur malveillant encore actif.

### 3. Logs système et applicatifs

- **Event Viewer** : outil natif Windows pour consulter les logs système.
- **Risque d'écrasement** : taille de fichier par défaut limitée → Windows supprime les logs les plus anciens une fois cette taille atteinte. La simple connexion/action d'un analyste peut générer de nouveaux logs qui écrasent d'anciens logs précieux.
  - **Action prioritaire** : copier immédiatement `%SystemRoot%\System32\winevt\` avant toute autre manipulation.
- **Logs hors Event Log** : certains services Microsoft n'utilisent pas l'Event Log standard :
  - DNS Server → `%SystemRoot%\System32\Dns\Dns.log`
  - DHCP Server → `%SystemRoot%\System32\dhcp\DhcpSrv.log`
- **Répertoires temporaires** : données utiles mais supprimables à la fermeture des applications → copier avant de terminer une application. Emplacements par défaut :
  - `%SystemRoot%\Temp`
  - `%UserProfile%\AppData\Local\Temp`
  - `C:\Users\<user_name>\AppData\Roaming\Temp`
  - `%ProgramData%\Temp`
- **Applications tierces** : emplacement des logs déterminé par l'application elle-même → identifier chaque application utilisée et localiser ses logs spécifiquement.

### 4. Windows Registry

Base de données des réglages système et préférences utilisateur — une copie documente la configuration exacte du système au moment de l'acquisition.

### Points de vigilance

- Éviter toute opération dégradant les performances ou modifiant durablement le système.
- Respecter le cadre légal et éthique (données personnelles).

## Questions / Réponses

**1. What is the data acquisition process performed while the system is running (e.g. during a security breach)?**
→ **Live Data Acquisition**

**2. What is the name of the tool used to examine system events occurring in Microsoft Windows, which comes pre-installed on Windows?**
→ **Event Viewer**
