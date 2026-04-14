# BrainOS — Schema

BrainOS est un wiki personnel maintenu par le LLM. Tu apportes les sources et poses les questions. Le LLM fait tout le reste.

## Qui tu es

[TON NOM] — [TON RÔLE / TA DESCRIPTION EN 1-2 PHRASES].
Stack : [TES OUTILS PRINCIPAUX]. Objectifs : [TES OBJECTIFS].
Domaines principaux : [DOMAINE 1], [DOMAINE 2], [DOMAINE 3].

---

## Architecture

```
BrainOS/
├── raw/                → Drop zone sources externes (immutable — LLM lit, ne modifie jamais)
│   └── assets/         → Images téléchargées localement
├── wiki/               → Savoir compilé — LLM écrit, tu lis
│   ├── sources/        → Résumés de sources (1 page = 1 source)
│   ├── topics/         → Connaissance domaine
│   ├── concepts/       → Modèles mentaux, frameworks, idées
│   ├── entities/       → Personnes, entreprises, outils, projets
│   ├── synthesis/      → Analyses cross-domaines + réponses archivées
│   └── decisions/      → Décisions importantes + contexte
├── daily/              → Notes quotidiennes (tu écris, LLM extrait)
├── outputs/            → Livrables générés
│   ├── drafts/
│   ├── analyses/
│   └── exports/
├── index.md            → Catalogue global du wiki (LLM maintient)
├── log.md              → Journal chronologique append-only (LLM maintient)
└── CLAUDE.md           → Ce fichier — schema, conventions, workflows
```

---

## Session loading

**À chaque session**, lire dans cet ordre :
1. `index.md` — vue d'ensemble du wiki, pages disponibles
2. `grep "^## \[" log.md | tail -10` — 10 dernières opérations

Ces deux fichiers remplacent tout Fast Memory. Ils sont toujours à jour.

---

## Opérations

### Ingest

Déclenchée par `/analyze [source]` (URL, fichier local, chemin raw/).

Flux recommandé (mode impliqué) :
1. Extraire le contenu brut (agent `source-extractor`)
2. **Discuter avec l'utilisateur** — thèse, points clés, angle à retenir
3. Écrire la page `wiki/sources/` (skill `write-source`)
4. Toucher les pages `topics/` et `concepts/` pertinentes (agent `wiki-integrator`)
5. Créer/mettre à jour les pages `entities/` mentionnées (skill `write-entity`)
6. Mettre à jour `index.md` (skill `update-index`)
7. Appender à `log.md` (skill `append-log`)

Mode batch (sans discussion) : exécuter les étapes 1, 3–7 sans pause.

Une source peut toucher 5 à 15 pages wiki. C'est normal.

### Query

Déclenchée par `/brain [question]`.

Flux :
1. Lire `index.md` pour identifier les pages pertinentes
2. Lire les pages ciblées
3. Synthétiser la réponse avec citations wiki (`[[page]]`)
4. **Proposer d'archiver** la réponse dans `wiki/synthesis/` si elle est non-triviale

Les bonnes réponses sont des pages wiki. Elles ne doivent pas disparaître dans l'historique de chat.

### Lint

Déclenchée par `/lint`.

L'agent `wiki-auditor` cherche :
- Pages orphelines (aucun lien entrant)
- Concepts mentionnés mais sans page dédiée
- Contradictions entre pages
- Données périmées (sources > 6 mois sur des sujets qui évoluent vite)
- Cross-références manquantes évidentes
- Suggestions de nouvelles sources à chercher

---

## Conventions

### Langue
- Français dans le wiki, sauf termes techniques
- Markdown Obsidian — wikilinks `[[page]]`, callouts `> [!note]`, frontmatter YAML

### Nommage des fichiers
- kebab-case, minuscules, 2–4 mots
- Pas de préfixe redondant avec le dossier parent
- `wiki/topics/webflow-cms.md` ✅ — pas `wiki/topics/topic-webflow-cms.md` ❌

### Frontmatter obligatoire

```yaml
---
title: "Titre lisible"
type: source | topic | concept | entity | synthesis | decision
domain: [ton domaine 1] | [ton domaine 2] | business | autre
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 1
---
```

Pour `entity`, ajouter : `entity_type: person | company | tool | project`
Pour `source`, ajouter : `source_url: ""` et `source_author: ""`

### Liens
- Toujours lier bidirectionnellement : si A mentionne B, B mentionne A
- Maximum 5 wikilinks par page (hors section "Connexions")
- Section "Connexions" en bas de page pour les liens secondaires

### Index
`index.md` est un **hub de navigation** — il pointe vers les `--index-*` par dossier, pas vers les pages individuelles.

Chaque dossier wiki a un fichier `--index-[nom].md` qui liste le contenu détaillé avec une phrase de résumé par page.

À chaque ingest, mettre à jour :
1. Le `_Index` du dossier concerné (ajouter la ligne de la nouvelle page)
2. Le compteur dans `index.md` si nécessaire

Format d'une ligne dans un `_Index` :
```
| [[slug-page]] | description une ligne | YYYY-MM-DD |
```

### Log
Format d'un en-tête dans `log.md` :
```
## [YYYY-MM-DD] <operation> | <titre>
```
Opérations valides : `ingest` · `query` · `lint` · `daily` · `end-session` · `init`

---

## Permissions

| Zone | Claude lit | Claude écrit | Notes |
|---|---|---|---|
| `raw/` | ✅ | ✅ (supprime après ingest si demandé) | Sources immutables |
| `wiki/` | ✅ | ✅ | Enrichissement continu |
| `daily/` | ✅ | ✅ (via /daily uniquement) | Ne modifie jamais une note existante |
| `outputs/` | ✅ | ✅ | Livrables sur demande |
| `index.md` | ✅ | ✅ | Mis à jour à chaque ingest |
| `log.md` | ✅ | ✅ (append only) | Ne jamais modifier une entrée |
| `.obsidian/` | ❌ | ❌ | Jamais toucher |

---

## Interdits

- Ne jamais modifier une entrée existante dans `log.md`
- Ne jamais supprimer un fichier `raw/` sans avoir créé la page `wiki/sources/` correspondante
- Ne jamais créer de doublon — vérifier `index.md` avant toute création
- Ne jamais modifier `.obsidian/`
- Ne pas créer de fichiers hors des zones autorisées sans demande explicite
- **Ne jamais créer une page vide** — toute page wiki doit avoir du contenu substantiel dès sa création

---

## Self-improvement

Après toute correction de comportement :
1. Identifier la règle générale derrière la correction
2. Mettre à jour ce CLAUDE.md ou les fichiers `.claude/` concernés
3. Ne pas répéter la même erreur
