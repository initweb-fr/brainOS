# BrainOS — Template clonable

> Un Second Brain vivant, maintenu par Claude. Tu apportes les sources et les questions. Claude fait le reste — lecture, structuration, connexions, synthèses.

Inspiré du pattern *[LLM Wiki](https://karpathy.bearblog.dev/llm-wiki/)* d'Andrej Karpathy.

---

## Démarrage rapide

👉 **Ouvre le dossier [README/](README/) et suis les 5 étapes dans l'ordre.**

- [00 — Commence ici](README/00-start-here.md)
- [01 — Installation](README/01-installation.md)
- [02 — Configure ton cerveau](README/02-configure-your-brain.md)
- [03 — Ta première source](README/03-first-ingest.md)
- [04 — Aller plus loin](README/04-going-further.md)
- [99 — Nettoyage](README/99-cleanup.md)

Compte **30 à 45 minutes** pour tout installer et faire ta première ingestion.

---

## En une phrase

Tu n'écris plus de notes. Tu dis à Claude *"tiens, regarde cet article"* — il le lit, en sort un résumé, crée ou met à jour 5 à 15 pages de ton wiki interconnecté. Au fil des semaines, tu poses des questions à ton propre savoir accumulé.

---

## Prérequis

- [Obsidian](https://obsidian.md) (gratuit)
- [Visual Studio Code](https://code.visualstudio.com) (gratuit)
- [Claude Code](https://docs.claude.com/en/docs/claude-code) + abonnement Claude Pro ou Max

Tout est détaillé dans [01-installation.md](README/01-installation.md).

---

## Structure du projet

```
BrainOS/
├── README/             → Guide de démarrage (à supprimer après onboarding)
├── raw/                → Dépose tes sources brutes ici
├── wiki/               → Savoir compilé — Claude écrit, tu lis
│   ├── sources/        → Résumés de sources (1 page = 1 source)
│   ├── topics/         → Connaissance par domaine
│   ├── concepts/       → Modèles mentaux, frameworks, idées
│   ├── entities/       → Personnes, entreprises, outils, projets
│   ├── synthesis/      → Analyses cross-domaines + réponses archivées
│   └── decisions/      → Décisions importantes + contexte
├── daily/              → Notes quotidiennes (tu écris, Claude extrait)
├── outputs/            → Livrables générés
├── index.md            → Catalogue global du wiki (Claude maintient)
├── log.md              → Journal chronologique (Claude maintient)
└── CLAUDE.md           → Schéma du système (configuré à l'étape 02)
```

---

## Commandes

| Commande | Ce que ça fait |
|---|---|
| `/analyze [source]` | Ingère une URL, un PDF, un fichier, ou un texte collé |
| `/brain [question]` | Interroge ton wiki avec citations |
| `/daily` | Crée la note du jour |
| `/transcript [fichier]` | Traite un transcript d'appel ou de réunion |
| `/lint` | Audite le wiki (orphelins, contradictions, lacunes) |
| `/end-session` | Clôture de session avec rapport |

---

## Licence & contribution

Fork libre, adapte à ton usage. Issues et PR bienvenues.

*Créé et maintenu par [Théo Roland](https://initweb.fr).*
