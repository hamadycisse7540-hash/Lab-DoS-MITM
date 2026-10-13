# Lab — Attaques par déni de service (DoS) et Man-in-the-Middle (MITM)

Rapport de laboratoire réalisé dans le cadre du **Mentorat Cybersécurité CYB6 (FORCE N)**.
Travaux pratiques de cybersécurité offensive menés sur un laboratoire **isolé** (réseau
VirtualBox host-only `192.168.56.0/24`), puis analyse des contre-mesures défensives.

> ⚠️ Toutes les manipulations ont été effectuées sur des machines virtuelles volontairement
> vulnérables, dans un environnement fermé et sans accès Internet, à des fins strictement
> pédagogiques. N'effectuez jamais ces techniques sur un système sans autorisation écrite.

## Environnement

| Machine | Rôle | IP |
|---|---|---|
| Kali Linux | Attaquant | `192.168.56.10` |
| Metasploitable 2 | Cible / serveur DVWA | `192.168.56.30` |
| Windows 7 | Victime | `192.168.56.20` |

## Contenu du lab

1. **Tâche 1 — DoS avec Scapy** : forge de paquets ICMP et envoi massif.
2. **Tâche 2 — Analyse Wireshark** : capture et lecture du trafic ICMP.
3. **Tâche 3 — SYN flood** (Metasploit + hping3) : démonstration de l'impact et des
   défenses de la pile TCP/IP (SYN cookies, rp_filter, RST du noyau).
4. **Tâche 4 — Sniffing** : interception des identifiants DVWA en HTTP clair.
5. **Tâche 5 — MITM par ARP spoofing** (Ettercap) : empoisonnement ARP et interception
   du trafic de la victime.
6. **Annexe** : récapitulatif des commandes utilisées, de leurs rôles et de leurs options.

## Structure du dépôt

```
.
├── Rapport_Lab_DoS_MITM.tex       # Source LaTeX du rapport
├── Rapport_Lab_DoS_MITM.pdf       # Rapport compilé
├── Rapport_Lab_DoS_MITM.pdf.asc   # Signature GPG détachée du PDF
├── HAMADY_CISSE_public_key.asc    # Clé publique GPG de l'auteur
├── images/                        # Captures d'écran du lab
├── LICENSE
└── README.md
```

## Compilation

```bash
pdflatex Rapport_Lab_DoS_MITM.tex
pdflatex Rapport_Lab_DoS_MITM.tex   # 2e passe pour le sommaire et l'annexe
```

## Vérifier l'authenticité

Le PDF du rapport est signé numériquement (GPG). Pour confirmer qu'il vient bien de l'auteur
et qu'il n'a pas été modifié :

```bash
# 1. Importer la clé publique de l'auteur
gpg --import HAMADY_CISSE_public_key.asc

# 2. Vérifier la signature détachée du PDF
gpg --verify Rapport_Lab_DoS_MITM.pdf.asc Rapport_Lab_DoS_MITM.pdf
```

La vérification doit afficher `Good signature from "HAMADY CISSE ..."`. L'empreinte de la clé
est :

```
A6F4 0DFD EE3E B7AE 80B3  6E77 361C 9E02 B790 303E
```

Les commits de ce dépôt sont eux aussi signés avec cette clé (badge « Verified » sur GitHub).

## Auteur

HAMADY CISSE — Mentorat Cybersécurité CYB6, Groupe 3.

## Licence

© 2026 HAMADY CISSE. Ce travail est publié sous licence
**[Creative Commons Attribution - Pas d'Utilisation Commerciale 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)**.

Vous pouvez partager et adapter ce travail **à des fins non commerciales**, à condition
de **créditer l'auteur**. Voir le fichier [`LICENSE`](LICENSE) pour les termes complets.
