# BrainOS — Mémoire projet

> Règles, corrections de comportement et préférences spécifiques à ce projet.
> Ce fichier complète `CLAUDE.md` (schema) et `log.md` (historique).
> Lu en début de session après `index.md` et `log.md`.

---

## Comportements corrigés

### /analyze sans argument → scanner raw/
**Date :** 2026-04-14
**Règle :** `/analyze` sans argument doit scanner et traiter tous les fichiers de `raw/` (hors `raw/assets/`), plutôt que demander à l'utilisateur de préciser une source.
**Pourquoi :** Correction explicite de l'utilisateur lors de la session d'initialisation.
**Application :** La commande [.claude/commands/analyze.md](.claude/commands/analyze.md) a été mise à jour en conséquence (étape 2 — Résolution de la source).

---

## Préférences d'ingest

*(à compléter au fil des sessions)*

---

## Conventions locales

*(à compléter si des exceptions aux règles globales de CLAUDE.md émergent)*
