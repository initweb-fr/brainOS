---
name: write-source
description: Écrire une page wiki/sources/ à partir du rapport de source-extractor et des notes de discussion avec l'utilisateur. Utilise cette skill UNIQUEMENT après extraction et discussion.
---

# write-source

## Quand l'utiliser

Uniquement dans un flux `/analyze` :
- Après que `source-extractor` a extrait le contenu brut
- Après discussion avec l'utilisateur sur la thèse et l'angle à retenir (en mode impliqué)
- Ou en mode batch, directement après extraction

## Structure d'une page source

```markdown
---
title: "Titre lisible de la source"
type: source
domain: [domaine principal]
tags: [tag1, tag2, tag3]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 1
source_url: "https://..."
source_author: "Nom auteur ou éditeur"
source_date: "YYYY-MM-DD"  # date de publication de la source
source_type: article | vidéo | podcast | pdf | livre | tweet
---

# Titre de la source

> [!quote] Thèse centrale
> Une phrase qui résume l'argument principal de la source.

## Contexte

Pourquoi cette source a été ingérée, dans quel contexte elle s'inscrit, quel problème elle adresse.

## Points clés

1. **Point 1** — développement court
2. **Point 2** — développement court
3. **Point 3** — développement court

(3 à 7 points, pas plus. Si plus, c'est que tu fais du résumé passif au lieu d'extraire l'angle.)

## Ce que j'en retiens

Angle personnel, lecture critique, liens avec les autres pages du wiki. **C'est la section la plus précieuse** — ce qui transforme une source en savoir activé.

## Citations notables

> Citation 1

> Citation 2

## Connexions

- [[topic-concerné-1]]
- [[concept-évoqué-1]]
- [[entité-mentionnée-1]]
```

## Règles

- **Slug** : kebab-case, 2–4 mots, évoque le sujet pas le format. `webflow-cms-patterns` ✅ — `article-medium-2024` ❌
- Emplacement : `wiki/sources/[slug].md`
- Le frontmatter est obligatoire et complet. Pas de champs vides sauf `source_date` si inconnue.
- Langue : français. Citations peuvent rester dans la langue d'origine si c'est une formule marquante.
- La section "Ce que j'en retiens" doit exister et avoir du contenu. Sans elle, la page n'a pas de valeur.
- Si la source est longue (livre, long podcast) : structurer "Points clés" en sous-sections par chapitre/partie.

## Vérifications avant écriture

1. Le slug n'existe pas déjà dans `wiki/sources/` (utiliser `Glob`)
2. Le frontmatter respecte le schéma `CLAUDE.md`
3. Minimum 300 mots de contenu (hors frontmatter et citations)

## Ce que tu ne fais PAS ici

- Tu n'ajoutes pas la ligne à `wiki/sources/--index-sources.md` (c'est le job de `update-index`)
- Tu ne touches pas aux autres pages wiki (c'est `wiki-integrator`)
- Tu n'appendes pas au log (c'est `append-log`)

Une fois la page écrite, retourne le chemin complet pour la suite du flux.
