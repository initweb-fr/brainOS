---
description: Ingérer une source (URL, fichier local, chemin raw/) dans le wiki BrainOS
argument-hint: [URL | chemin fichier | "batch"]
---

# /analyze — Ingest d'une source dans BrainOS

**Source à ingérer** : $ARGUMENTS

## Flux à exécuter

### 1. Session loading (si pas déjà fait dans cette session)

Lire dans cet ordre :
- `index.md`
- Les 10 dernières opérations : `grep "^## \[" log.md | tail -10`

### 2. Résolution de la source

- Si `$ARGUMENTS` est non vide → utiliser cette valeur comme source.
- Si `$ARGUMENTS` est vide → scanner le dossier `raw/` (Glob `raw/**/*`, hors `raw/assets/`).
  - Si `raw/` contient plusieurs fichiers, les lister à l'utilisateur et ingérer chacun en séquence.
  - Si `raw/` est vide, informer l'utilisateur qu'il n'y a rien à ingérer.

### 3. Extraction

Invoquer l'agent `source-extractor` avec la source.
Récupérer son rapport (métadonnées + contenu + points clés + entités).

### 4. Discussion (mode impliqué — par défaut)

**Par défaut, parler à l'utilisateur avant d'écrire quoi que ce soit** :
- Résumer la thèse en 2–3 phrases
- Proposer 3–5 points clés candidats
- Proposer un angle personnel ("ce qu'on en retient")
- Demander : accord ? ajouts ? angle différent ?

**Mode batch** : si l'utilisateur a passé `batch` en argument ou demande explicitement "pas de discussion", sauter cette étape et exécuter directement la suite avec un angle neutre.

### 5. Écriture de la page source

Utiliser la skill `write-source` pour créer `wiki/sources/[slug].md` à partir du rapport d'extraction + décisions de la discussion.

### 6. Intégration wiki

Invoquer l'agent `wiki-integrator` avec le chemin de la page source.
Il crée/enrichit les pages `topics/` et `concepts/` pertinentes, pose les liens bidirectionnels.

### 7. Entités

Pour chaque entité notable identifiée à l'étape 3, utiliser la skill `write-entity` (création ou mise à jour).

### 8. Mise à jour des index

Utiliser la skill `update-index` pour :
- Ajouter la ligne dans les `--index-*.md` des dossiers touchés
- Mettre à jour les compteurs de `index.md`

### 9. Log

Utiliser la skill `append-log` avec `operation: ingest` et un titre court évoquant la source.

### 10. Nettoyage raw/ (optionnel)

Si la source provenait de `raw/`, demander à l'utilisateur s'il veut supprimer le fichier source (il est maintenant capturé dans `wiki/sources/`).

## Règles

- **Une source peut toucher 5 à 15 pages wiki**, c'est normal et attendu.
- Ne jamais créer de page vide (min. 150 mots pour entités/concepts/topics, 300 pour sources).
- Toujours vérifier `index.md` avant création pour éviter les doublons.
- Respecter strictement les conventions de nommage et frontmatter définies dans `CLAUDE.md`.
- À la fin, retourner un récap court : pages créées, pages mises à jour, prochaines pistes d'ingest éventuelles.
