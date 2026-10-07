# BACKEND SCHEMA — Roadmap Cybersécurité enrichie

> Ce dépôt est une **base de connaissances**, pas une application : les rubriques techniques (flux, schéma, design) décrivent ici la structure du contenu, son parcours de lecture et ses conventions de rédaction.

## 1. Arborescence

```
Roadmap-cyber/
├── README.md                    # présentation du dépôt
├── Cybersecurite-Roadmap.md     # MOC : tout le contenu
└── (documentation : PRD, TRD, APP_FLOW, DESIGN_BRIEF, BACKEND_SCHEMA, IMPLEMENTATION_PLAN)
```

## 2. Schéma du frontmatter

```yaml
---
title: "Cybersécurité — Roadmap enrichie"   # titre affiché
aliases: ["Roadmap Cyber", ...]             # noms alternatifs (recherche Obsidian)
tags: [cybersécurité, roadmap, moc, ...]    # filtres
source: "https://roadmap.sh/cyber-security" # source principale
created: 2026-10-07                         # date de création
status: en-cours                            # en-cours | stable
---
```

## 3. Schéma d'une section

```
## N. <emoji> <Domaine>
> [!IMPORTANT] idée directrice du domaine
### <Sous-partie> <🟢|🟡|🔴>
- définition / fonctionnement
| tableau | si énumération |
> [!TIP] / [!WARNING]
---
```

## 4. Schéma prévu des notes atomiques

```yaml
---
title: "<Notion>"
domaine: reseau | systeme | crypto | attaques | cloud | gouvernance | outils
niveau: fondamental | intermediaire | avance
tags: []
liens: ["[[Notion voisine]]"]
---
```
