# DFIR Learning Path

> Mon parcours d'apprentissage en **DFIR** — *Digital Forensics & Incident Response*.
> Notes, méthodologie et ressources pour l'investigation numérique et la réponse à incident.

<p align="left">
  <img src="https://img.shields.io/badge/Focus-DFIR-2b6cb0?style=flat-square">
  <img src="https://img.shields.io/badge/Blue%20Team-SOC-4a5568?style=flat-square">
  <img src="https://img.shields.io/badge/Status-En%20cours-6b46c1?style=flat-square">
</p>

---

## Objectif

Développer une méthodologie solide de **réponse à incident** et d'**analyse forensique**
pour appuyer mon parcours d'analyste SOC / Blue Team.

---

## Domaines couverts

- **Incident Response** — cycle de réponse à incident (préparation, identification,
  confinement, éradication, remédiation, retour d'expérience)
- **Disk Forensics** — analyse de systèmes de fichiers, artefacts, fichiers supprimés
- **Memory Forensics** — analyse de dumps mémoire (Volatility)
- **Windows Forensics** — registre, Event Logs, MFT, prefetch, artefacts d'exécution
- **Network Forensics** — analyse de captures (Wireshark, PCAP)
- **Timeline & Triage** — reconstruction chronologique, collecte de preuves

---

## Méthodologie de réponse à incident

| Phase | Description |
|-------|-------------|
| **1. Préparation** | Outils, procédures et environnement prêts |
| **2. Identification** | Détecter et qualifier l'incident |
| **3. Confinement** | Limiter la propagation |
| **4. Éradication** | Supprimer la cause racine |
| **5. Remédiation** | Restaurer les systèmes sains |
| **6. Leçons apprises** | Documenter et améliorer |

---

## Outils

- **Forensics** : Autopsy, FTK Imager, Volatility, plaso / log2timeline
- **Windows** : Event Viewer, Registry Explorer, Eric Zimmerman tools
- **Réseau** : Wireshark, tcpdump, NetworkMiner
- **Analyse** : VirusTotal, YARA

---

## Structure du dépôt

```text
dfir-learning-path/
├── incident-response/    # Notes et procédures IR
├── disk-forensics/       # Analyse disque
├── memory-forensics/     # Analyse mémoire (Volatility)
├── windows-forensics/    # Artefacts Windows
├── network-forensics/    # Analyse réseau / PCAP
└── resources/            # Liens, cheat sheets, références
```

---

## Ressources

- [DFIR.training](https://www.dfir.training/)
- [SANS DFIR Posters & Cheat Sheets](https://www.sans.org/posters/?focus-area=digital-forensics)
- [Volatility Foundation](https://www.volatilityfoundation.org/)
- [Eric Zimmerman's Tools](https://ericzimmerman.github.io/)

---

## Auteur

**Maimouni Mohammed** — Étudiant en cybersécurité, orientation SOC / Blue Team
[GitHub](https://github.com/simohowaanaa) · [LinkedIn](https://www.linkedin.com/in/mohammed-maimouni/)
