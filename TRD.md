# TRD — Roadmap Cybersécurité enrichie

> Ce dépôt est une **base de connaissances**, pas une application : les rubriques techniques (flux, schéma, design) décrivent ici la structure du contenu, son parcours de lecture et ses conventions de rédaction.

## 1. Format

| Élément | Choix | Raison |
|---|---|---|
| Fichier | Markdown unique `Cybersecurite-Roadmap.md` (MOC) | Point d'entrée unique, diffable dans git |
| Métadonnées | Frontmatter YAML (`title`, `aliases`, `tags`, `source`, `created`, `status`) | Recherche et graphe Obsidian |
| Mise en valeur | Callouts `> [!NOTE]`, `[!TIP]`, `[!WARNING]`, `[!IMPORTANT]` | Rendus nativement par GitHub **et** Obsidian |
| Navigation | Sommaire à ancres | Navigation dans un long document |
| Données denses | Tableaux Markdown | Lecture en diagonale |
| Code | Blocs de code avec langage | Commandes copiables |

## 2. Outils

- **Lecture** : GitHub (rendu web) ou [Obsidian](https://obsidian.md) (dossier ouvert comme coffre).
- **Édition** : tout éditeur Markdown ; prévisualiser dans les deux rendus avant de publier.

## 3. Compatibilité

- Les ancres du sommaire suivent la génération d'ancres de GitHub (emojis et accents compris) : vérifier qu'un lien du sommaire fonctionne après renommage d'un titre.
- Éviter la syntaxe propre à Obsidian (`[[wikilinks]]`, `![[intégrations]]`) dans le MOC tant qu'il doit rester lisible sur GitHub ; la réserver aux notes atomiques.

## 4. Qualité

- Toute affirmation sensible (CVE, version, commande destructrice) est vérifiée avant publication.
- Les sources externes sont citées par lien.
