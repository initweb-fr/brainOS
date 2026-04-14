---
name: append-log
description: Appender une entrée dans log.md pour tracer une opération (ingest, query, lint, daily, end-session, init). Append-only, jamais de modification d'entrée existante.
---

# append-log

## Quand l'utiliser

À la fin de toute opération notable :
- `ingest` — après un `/analyze` complet
- `query` — après un `/brain` si la réponse a été archivée
- `lint` — après un `/lint`
- `daily` — après un `/daily`
- `end-session` — à la demande explicite (`/end-session`)
- `init` — initialisation du vault

## Format strict

Entête :
```
## [YYYY-MM-DD] <operation> | <titre court>
```

Corps (1 paragraphe ou quelques bullets) :
- Quoi : objet de l'opération
- Pages touchées (avec wikilinks)
- Décisions ou points notables à retenir

Exemple :

```
## [2026-04-14] ingest | Article Paul Graham sur les essais

- Source : [[wiki/sources/pg-essays-writing]]
- Topics touchés : [[topics/ecriture]], [[topics/idees-produit]]
- Concepts créés : [[concepts/writing-is-thinking]]
- Entités : [[entities/paul-graham]] (mise à jour, +1 source)
- Angle retenu : l'écriture force la clarté de pensée, utile pour la phase de cadrage produit.
```

## Règles absolues

1. **APPEND ONLY** — on ajoute au-dessus de la dernière entrée (ordre antichronologique : plus récent en haut). **Ne jamais modifier ou supprimer une entrée existante.**
2. Respecter strictement le format de l'entête (pour que `grep "^## \[" log.md` fonctionne lors du session-loading).
3. Date au format `YYYY-MM-DD`. Pas d'heure, pas de fuseau.
4. Operation = un seul mot dans la liste valide.
5. Titre court = max 8 mots, pas de ponctuation en fin.

## Emplacement dans le fichier

La structure de `log.md` :
```
# BrainOS — Log

> Journal chronologique append-only. Entrées les plus récentes en premier.
> Ne jamais modifier une entrée existante.

---

## [date récente] operation | titre
...

## [date précédente] operation | titre
...
```

**Insertion** : après la ligne `---` et avant l'entrée la plus récente précédente.

## Algorithme

1. `Read log.md`
2. Construire l'entrée avec date du jour + opération + titre.
3. `Edit` pour insérer juste après la ligne `---` et un saut de ligne, avant le `## [` suivant.
4. Vérifier qu'aucune entrée existante n'a été modifiée.

## Ce que tu ne fais PAS

- Ne jamais reformater une entrée antérieure, même si le format est imparfait (historique immuable).
- Ne jamais supprimer une entrée.
- Ne pas ajouter deux entrées pour la même opération — consolider en une seule avec toutes les infos.
