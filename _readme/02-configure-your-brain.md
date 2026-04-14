# 02 — Configure ton cerveau

> L'étape la plus importante. Ton BrainOS doit **te connaître**. Un système générique est inutile — un système qui sait **qui tu es, ce que tu cherches, comment tu penses** devient un vrai multiplicateur.

Plutôt que de te faire remplir des formulaires, on va laisser Claude **t'interviewer pendant 10-15 minutes**. Il te posera des questions, tu répondras naturellement, et à la fin il écrira tout seul un fichier `CLAUDE.md` adapté à toi.

Ce fichier, c'est le "mode d'emploi" que Claude utilisera à chaque session pour se souvenir de qui tu es.

---

## Comment faire — pas à pas

### 1. Ouvre une session Claude via l'extension Claude de VS Code.

Ouvre l'extension Claude, démarre une nouvelle session. Une page de discussion avec Claude s'ouvre.

### 2. Copie le gros prompt plus bas

Sélectionne **tout le bloc de code grisé** dans la section "Le prompt d'interview" juste en dessous (du premier au dernier tiret). Copie-le (Cmd/Ctrl + C).

### 3. Colle-le dans Claude

Retourne dans l'extension Claude Code dans VS Code, clique dedans, colle (Cmd/Ctrl + V), puis appuie sur Entrée.

### 4. Laisse-toi interviewer

Claude va te poser des questions une par une. **Réponds honnêtement, sans chercher à bien formuler.** Si une question te semble floue, demande à Claude de préciser. Si tu te trompes, corrige-toi — il comprendra.

### 5. Valide à la fin

Quand Claude estime avoir assez de matière, il te fera un résumé de ce qu'il a compris. Lis-le, corrige ce qui n'est pas juste, puis dis-lui d'écrire ton `CLAUDE.md`.

---

## Le prompt d'interview

Copie tout le bloc ci-dessous, du premier au dernier tiret.

```
Tu es l'architecte de mon BrainOS. Avant de configurer quoi que ce soit, tu vas m'interviewer pour comprendre qui je suis et comment je pense — puis écrire un CLAUDE.md personnalisé qui te servira de schéma pour les prochaines années.

CONTEXTE POUR TOI

BrainOS est un pattern de Second Brain maintenu par toi (le LLM). L'humain apporte les sources et les questions. Tu fais le travail d'extraction, de structuration, de cross-référencement et de synthèse. Le wiki vit dans `wiki/` et s'enrichit à chaque ingest. Le fichier `CLAUDE.md` que tu vas produire est la seule chose qui te distingue d'un chatbot générique : il te dit comment penser, quoi privilégier, quel vocabulaire utiliser, quels domaines sont prioritaires.

Le CLAUDE.md actuel est un template avec des placeholders. Ton job est de le remplacer par une version qui reflète vraiment la personne en face de toi.

TON RÔLE PENDANT L'INTERVIEW

- Pose tes questions UNE À LA FOIS, pas en batch. Attends ma réponse avant la suivante.
- Reformule après chaque réponse pour vérifier que tu as bien compris ("donc si je résume…"). Je corrige si besoin.
- Creuse quand une réponse est vague. Une interview superficielle produit un CLAUDE.md superficiel.
- Si je dis quelque chose de surprenant ou contradictoire, note-le mentalement — ça fera partie de ma singularité à capturer.
- N'écris RIEN dans les fichiers avant la fin de l'interview. Pas de mise à jour intermédiaire. Sauf si je te demande explicitement de sauvegarder ce qui a été partagé ou de mettre en pause.

CE QUE TU DOIS APPRENDRE (dans cet ordre, adapte selon mes réponses)

1. IDENTITÉ — prénom, rôle actuel (pro et perso si pertinent), contexte de vie en une phrase. Est-ce que je dirige un projet, une entreprise, une équipe ? Suis-je salarié, freelance, fondateur, étudiant ?

2. POURQUOI BRAINOS — qu'est-ce que j'essaie d'accumuler et pourquoi ? Qu'est-ce qui m'a manqué dans mon système précédent (Notion, Apple Notes, rien, etc.) ? Quel type de question j'aimerais pouvoir poser à mon cerveau dans 6 mois ?

3. DOMAINES — 2 à 4 grands territoires de connaissance que je veux cultiver. Pas des mots creux ("productivité") — des domaines opérationnels ("architecture de scénarios Make", "psychologie des fondateurs solo", "copywriting SaaS B2B"). Pour chacun, demande ce qui m'intéresse précisément et ce qui ne m'intéresse pas.

4. STACK — outils que j'utilise quotidiennement ou que je maîtrise. Ça t'aide à calibrer le niveau technique de tes explications et à faire des ponts pertinents.

5. OBJECTIFS 6–12 MOIS — 2 ou 3 choses concrètes que je veux accomplir. Ça te permettra plus tard de repérer quand une source est particulièrement pertinente pour mes priorités.

6. STYLE DE PENSÉE ET DE TRAVAIL — est-ce que je préfère les synthèses ultra-courtes ou les analyses creusées ? Les bullet points ou les paragraphes ? Les frameworks ou les exemples concrets ? Le ton : direct et cash ou nuancé et diplomate ? Est-ce que j'aime être challengé ou j'attends que tu valides mes intuitions ?

7. LANGUE — français, anglais, mixte ?

8. CONTRAINTES OU INTERDITS — y a-t-il des sujets que je ne veux pas voir dans le wiki ? Des personnes, des entreprises, des outils à ne jamais mentionner ? Des modes de réponse qui m'agacent ("ne me propose jamais de faire de la méditation", "ne me donne pas des conseils génériques de LinkedIn", etc.) ?

9. NIVEAU DE SUPERVISION — quand tu ingères une source, est-ce que tu préfères discuter avec moi d'abord (mode impliqué) ou agir sans pause (mode batch) ?

APRÈS L'INTERVIEW

Quand tu as assez de matière (tu le sauras — l'image est nette), récapitule en 10–15 lignes ce que tu as compris de moi. Attends ma validation.

Puis réécris `CLAUDE.md` :
- Remplis la section "Qui tu es" avec mon profil réel (nom, rôle, contexte, domaines, objectifs)
- Ajoute en bas une section "Préférences" qui capture mon style (ton, format, longueur, ce qu'il faut éviter)
- Garde intact le reste (architecture, opérations, conventions, permissions, interdits) — c'est le socle
- Propose-moi une ou deux règles de plus si tu vois quelque chose de spécifique à mon cas qui mérite d'être codifié
- Crée un fichier profil-prenom-nom.md avec les informations détaillé que tu as retenu de mon interview.

Ensuite confirme que le fichier est prêt et invite-moi à passer à `README/03-first-ingest.md`.

Commence par te présenter en une phrase, puis pose ta première question.
```

---

## Pourquoi une interview plutôt qu'un formulaire

Si on te donnait un modèle avec des champs à remplir (*"ton domaine principal : ___"*), tu écrirais 3 mots et Claude n'aurait aucun contexte réel.

Une vraie conversation fait ressortir :
- Les nuances de tes domaines (ce qui t'intéresse **précisément**, ce qui ne t'intéresse pas)
- Ton vocabulaire à toi
- Les choses à éviter dans son style de réponse
- Des spécificités que tu n'aurais jamais pensé à écrire si on t'avait demandé

C'est la différence entre un questionnaire RH et une vraie discussion avec quelqu'un qui veut comprendre.

---

## Après l'interview

Ouvre ton `CLAUDE.md` dans Obsidian ou dans VS Code. Jette un œil à ce que Claude a écrit. Si une phrase te dérange, modifie-la directement (c'est un simple fichier texte) ou demande à Claude de la réécrire.

**Tu peux refaire l'interview plus tard.** Si ta vie change dans 6 mois (nouveau projet, nouveau métier, nouveaux centres d'intérêt), dis simplement à Claude :

> *"Refais l'interview de configuration, j'ai évolué."*

Il relancera le même processus et mettra ton fichier à jour.

---

## Ton prochain pas

→ **[03-first-ingest.md](03-first-ingest.md)** — ingérer ta première source et poser ta première question.
