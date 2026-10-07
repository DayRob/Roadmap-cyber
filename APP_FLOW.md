# APP FLOW — Roadmap Cybersécurité enrichie

> Ce dépôt est une **base de connaissances**, pas une application : les rubriques techniques (flux, schéma, design) décrivent ici la structure du contenu, son parcours de lecture et ses conventions de rédaction.

## 1. Parcours de lecture

```
README ──► Cybersecurite-Roadmap.md
             ├─ « Comment lire ce document » (callouts, criticité, Obsidian)
             ├─ Sommaire ──► domaine 1 … 12
             │     └─ sous-partie 🟢 / 🟡 / 🔴
             │           ├─ définition et fonctionnement
             │           ├─ tableau (ports, protocoles, attaques, outils)
             │           └─ callout : astuce, piège, à retenir
             └─ « Aller plus loin » ──► éclater en notes Obsidian
```

## 2. Parcours de révision recommandé

```
Fondamentaux (1, 2, 3) ──► Sécurité & crypto (4, 5) ──► Attaques (6)
   ──► Cloud & scripting (7, 8) ──► Cadres & outils (9, 10) ──► Certifs & CTF (11, 12)
Premier passage : seulement 🟢 · Deuxième : 🟡 · Approfondissement : 🔴
```

## 3. Parcours Obsidian

```
Cloner le dépôt ──► ouvrir le dossier comme coffre
  ──► le frontmatter alimente recherche et graphe
  ──► créer des notes atomiques ([[Triade CIA]], [[OWASP Top 10]], [[Kerberos]]…)
  ──► relier depuis le MOC ──► taguer par domaine (#réseau, #pentest, #blue-team)
```

## 4. Parcours de mise à jour

```
Nouvelle notion ou correction ──► section concernée ──► niveau 🟢/🟡/🔴
  ──► vérifier le rendu GitHub et Obsidian ──► mettre à jour le sommaire si un titre change ──► commit
```
