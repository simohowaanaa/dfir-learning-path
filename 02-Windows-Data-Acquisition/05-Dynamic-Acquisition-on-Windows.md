# Leçon 5 — Dynamic Acquisition on Windows

## Résumé

Introduction d'un troisième concept aux côtés du Live Data Acquisition : la **Dynamic Acquisition** — collecte de données précises, en continu ou en réponse à des événements, plutôt qu'une capture complète unique.

## Points clés

### Live Data Acquisition vs Dynamic Acquisition

| Aspect | Live Data Acquisition | Dynamic Acquisition |
|---|---|---|
| Définition | Copie de la mémoire et données volatiles d'un système en marche | Copie de données précises, à intervalles réguliers ou en réponse à événements |
| But | Capturer l'état complet de l'OS/programmes à l'instant T | Surveillance continue et capture ciblée, système reste opérationnel |
| Avantages | Plus de données récupérables (supprimées/altérées), infos sensibles exposées | Ne bloque/plante pas le système, moins d'expertise/outils requis, moins de temps/ressources |
| Inconvénients | Peut bloquer/planter le système, expertise et outils spécialisés, plus de temps | Moins complet, données supprimées non récupérables, infos sensibles potentiellement manquées |

Les deux approches sont complémentaires selon le contexte : Dynamic Acquisition = plus légère et moins risquée pour la stabilité, Live Data Acquisition = plus complète mais plus intrusive.

### 3 méthodes de Dynamic Acquisition

1. **System and Application Logs** : logs système/applicatifs/sécurité (événements, erreurs, activités utilisateur, brèches)
2. **Network Monitoring** : trafic et connexions réseau (détection de menaces/anomalies)
3. **Performance Monitoring** : métriques CPU, mémoire, I/O disque (optimisation, capacity planning)

### Outils (suite Sysinternals)

- **Process Explorer** : vue détaillée des processus, mémoire, ressources. Clic droit → changer priorité, terminer, suspendre, redémarrer, dumper. Onglets Properties : Image, TCP/IP, Strings, Performance, Security, Services.
- **AutoRuns** : scanne tous les mécanismes de démarrage automatique — crucial car les attaquants les exploitent pour la **persistance**. Affiche éditeur, signature, date d'installation, chemin, vérification VirusTotal.
- **Regedit** : lit/modifie/sauvegarde le Windows Registry. `File > Export` pour copier l'état actuel.
- **Security Tools** (ex. Windows Defender) : historiques de menaces/activités à copier lors d'une investigation. Attention : certains outils endpoint utilisent une gestion centralisée → il faut parfois accéder à la console de management plutôt qu'à la machine locale.

### Points de vigilance

- Confidentialité et conformité légale
- Performance système (la collecte dynamique consomme des ressources)

## Questions / Réponses

**1. What is the name of the tool that is installed by default in Windows and allows you to read, modify, and back up the Windows Registry database?**
→ **Regedit** — "'Regedit' is a tool that comes pre-installed with Windows and allows you to read/modify/backup this database [Windows Registry]."
