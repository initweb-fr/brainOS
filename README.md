# BrainOS

> **Un Second Brain vivant, maintenu par Claude.**
> Tu apportes les sources et les questions. Claude fait le reste.

BrainOS est un template clonable pour construire ta propre base de connaissances personnelle — un wiki qui grandit, se structure et se connecte tout seul au fil de ce que tu lis. Tu n'écris plus de notes. Tu ingères des sources, tu poses des questions, et Claude s'occupe du reste.

Inspiré du pattern *[LLM Wiki](https://karpathy.bearblog.dev/llm-wiki/)* d'Andrej Karpathy.

---

## Le problème

Prendre des notes, c'est fastidieux. Les ranger, c'est pire. Et après 6 mois, personne ne retrouve rien.

La plupart des systèmes de notes échouent pour la même raison : **le coût de maintenance dépasse la valeur perçue**. On arrête de relier, de mettre à jour, de classer. Le vault devient un cimetière de markdown.

Les outils comme ChatGPT avec upload de fichiers ou NotebookLM règlent une partie du problème (tu retrouves l'info), mais ils redécouvrent ta connaissance **à chaque question**. Rien ne s'accumule. Rien ne se structure.

## L'idée de BrainOS

Au lieu d'interroger des sources brutes à chaque fois, **Claude maintient un wiki persistant entre toi et tes sources**. Quand tu ajoutes une nouvelle source, Claude ne l'indexe pas — il la lit, en extrait les idées clés, et les **intègre dans le wiki existant** :

- Met à jour les pages entités concernées
- Révise les synthèses en cours
- Signale les contradictions avec ce que tu as déjà lu
- Renforce ou challenge les connexions

La connaissance est **compilée une fois** puis tenue à jour. Pas re-dérivée à chaque requête.

Après quelques semaines, ton wiki devient plus riche que ta propre mémoire sur les sujets que tu explores. Chaque nouvelle source enrichit 5 à 15 pages. Les connexions se font toutes seules. **Le wiki compound dans le temps.**

## Comment ça marche

Tu as deux fenêtres ouvertes côte à côte :

- **Obsidian** → tu lis ton wiki, tu navigues le graphe de connexions
- **Claude Code** → tu discutes avec Claude, il modifie les fichiers en direct

Trois opérations principales :

| Opération | Commande | Ce qui se passe |
|---|---|---|
| **Ingest** | `/analyze [source]` | Claude lit une URL, un PDF ou un fichier, discute avec toi, puis écrit 5–15 pages dans le wiki |
| **Query** | `/brain [question]` | Claude lit l'index du wiki, synthétise une réponse avec citations vers tes propres pages |
| **Lint** | `/lint` | Claude audite le wiki : pages orphelines, contradictions, concepts sans page dédiée, lacunes à combler |

Plus quelques utilitaires : `/daily` pour la note du jour, `/transcript` pour les réunions, `/end-session` pour clôturer une session de travail.

## Démarrage

**[Commence par le dossier `_readme/`](_readme/00-start-here.md)** — 5 étapes dans l'ordre, environ 30 à 45 minutes pour tout installer et faire ta première ingestion.

| Étape | Fichier | Durée |
|---|---|---|
| 00 | [Commence ici](_readme/00-start-here.md) | 5 min |
| 01 | [Installation](_readme/01-installation.md) | 15–25 min |
| 02 | [Configure ton cerveau](_readme/02-configure-your-brain.md) | 10–15 min |
| 03 | [Première source, première question](_readme/03-first-ingest.md) | 10 min |
| 04 | [Aller plus loin](_readme/04-going-further.md) | lecture libre |
| 99 | [Nettoyage](_readme/99-cleanup.md) | 1 min |

## Prérequis

- **[Obsidian](https://obsidian.md)** — gratuit — pour lire et naviguer le wiki
- **[Visual Studio Code](https://code.visualstudio.com)** — gratuit — pour discuter avec Claude
- **[Claude Code](https://docs.claude.com/en/docs/claude-code)** — abonnement Claude Pro ou Max requis
- **[Node.js](https://nodejs.org/en/download)** — gratuit — moteur nécessaire à Claude Code

Tout est détaillé dans [01-installation.md](_readme/01-installation.md), y compris pour les profils non-technophiles.

## Structure du projet

```
BrainOS/
├── _readme/            → Guide de démarrage (à supprimer après onboarding)
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

## À qui c'est destiné

BrainOS est utile pour n'importe qui accumule de la connaissance sur un sujet dans le temps :

- **Un indépendant ou fondateur** qui veut structurer sa veille métier
- **Un chercheur ou étudiant** qui creuse un sujet sur plusieurs mois
- **Un créateur de contenu** qui capitalise sur ses lectures et interviews
- **Une équipe** qui veut un wiki interne maintenu par un LLM, alimenté par Slack, transcripts, docs
- **Tout curieux** qui en a marre d'oublier 80 % de ce qu'il lit

Pas besoin d'être développeur. Le template est conçu pour être utilisé dès l'installation, sans écrire une ligne de code.

## Philosophie

> Le travail fastidieux d'une base de connaissances, ce n'est pas la lecture ou la réflexion — c'est le **bookkeeping**. Mettre à jour les cross-références, maintenir les résumés, signaler les contradictions, garder la cohérence entre des dizaines de pages. Les humains abandonnent les wikis parce que la maintenance grandit plus vite que la valeur. Les LLM ne s'ennuient pas, n'oublient pas, et peuvent toucher 15 fichiers d'un coup.
>
> *— Andrej Karpathy, [LLM Wiki](https://karpathy.bearblog.dev/llm-wiki/)*

Ton rôle : sourcer, explorer, poser les bonnes questions, décider ce que ça veut dire.
Le rôle de Claude : tout le reste.

## Contribution

Fork libre, adapte à ton usage, partage tes améliorations. Les issues et pull requests sont les bienvenues.

## Licence

MIT. Utilise comme tu veux.

## Crédits

- Pattern originel : [Andrej Karpathy](https://karpathy.bearblog.dev/llm-wiki/)
- Template maintenu par [Théo Roland](https://initweb.fr) — [initWeb](https://initweb.fr) / STUDIO ROLAND

---

*Si BrainOS t'aide, laisse une star sur le repo. Ça m'aide à savoir si ça sert à autre chose que mon propre cerveau.*
