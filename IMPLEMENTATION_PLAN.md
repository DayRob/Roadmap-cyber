# IMPLEMENTATION PLAN — Roadmap Cybersécurité enrichie

> Ce dépôt est une **base de connaissances**, pas une application : les rubriques techniques (flux, schéma, design) décrivent ici la structure du contenu, son parcours de lecture et ses conventions de rédaction.

## Phases

| # | Phase | Contenu | Statut |
|---|---|---|---|
| 1 | MOC | Les 12 domaines de roadmap.sh, enrichis, avec criticité et callouts | ✅ Fait |
| 2 | Relecture | Vérification des points sensibles (CVE, versions, commandes) | ⏳ À faire |
| 3 | Notes atomiques | Éclater les concepts clés en notes Obsidian reliées par `[[wikilinks]]` | ⏳ |
| 4 | Fiches commandes | nmap, tcpdump, PowerShell / Active Directory… | ⏳ |
| 5 | Writeups | Dossier `/writeups` pour les CTF (TryHackMe, HTB, Root Me) | ⏳ |
| 6 | Veille | Note « Veille » : flux RSS, comptes à suivre, CVE | ⏳ |
| 7 | Approfondissement | Infra sécurisée, pentest, chemins d'attaque Active Directory | ⏳ |

## Liens avec les autres projets

- **connaissance_transversale** : les notes atomiques peuvent y être publiées en open source.
- **Cybereduc** : ce contenu alimente la base du RAG qui génère les jeux éducatifs.
- **Study Copilot** : la note « Veille » rejoint la future veille cyber (CERT-FR, ANSSI).

## Définition de « terminé » pour une section

- [ ] Chaque sous-partie a son niveau 🟢/🟡/🔴
- [ ] Au moins une défense ou bonne pratique par attaque citée
- [ ] Rendu vérifié sur GitHub et dans Obsidian
- [ ] Sources citées
