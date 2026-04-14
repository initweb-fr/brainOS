# 01 — Installation

Temps estimé : **15 à 25 minutes**.

Pas de panique si tu n'es pas à l'aise avec la ligne de commande. Je te donne chaque étape mot pour mot.

---

## Ce qu'on va installer

Quatre outils. Chacun a un rôle précis :

| Outil                                 | À quoi il sert                                                                                                        |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Obsidian**                          | L'application où tu vas lire ton wiki. C'est comme un traitement de texte mais pour naviguer entre des pages reliées. |
| **Visual Studio Code** (ou "VS Code") | Une application qui sert ici à **parler à Claude dans un terminal intégré**. Tu n'as pas à apprendre à coder avec.    |
| **Node.js**                           | Un petit moteur invisible dont Claude Code a besoin pour fonctionner. Tu l'installes et tu oublies.                   |
| **Claude Code**                       | L'outil officiel d'Anthropic qui te permet de faire parler Claude avec tes fichiers.                                  |

Ajoute à ça **un abonnement Claude** (Pro ou Max, [claude.ai/pricing](https://claude.ai/pricing)). C'est la seule dépense.

---

## Étape 1 — Récupérer le template

Il y a trois façons de récupérer BrainOS sur ton ordinateur.

### Option A (la plus simple) — Télécharger un ZIP

1. Va sur la page GitHub du template
2. Clique sur le bouton vert **"Code"** en haut à droite
3. Clique sur **"Download ZIP"**
4. Dézippe le fichier quelque part de facile à retrouver, par exemple dans ton dossier **Documents**. Renomme le dossier en `BrainOS` (ou le nom que tu veux).

### Option B — Utiliser Github Desktop

### Option C — Utiliser Git (si tu connais)

Si tu sais ce qu'est Git :
```bash
git clone https://github.com/[TON_USER]/BrainOS-template.git BrainOS
```

> 💡 Tu peux mettre le dossier où tu veux : dans **Documents**, sur ton **Bureau**, etc. Évite iCloud ou Google Drive synchronisés — ça peut créer des conflits.

---

## Étape 2 — Installer Obsidian

Obsidian est gratuit pour un usage personnel.

1. Va sur [obsidian.md/download](https://obsidian.md/download)
2. Télécharge la version pour ton système (macOS, Windows ou Linux)
3. Installe-la comme n'importe quelle application

### Ouvrir ton BrainOS dans Obsidian

1. Lance Obsidian
2. Sur l'écran d'accueil, clique **"Ouvrir un dossier comme coffre"**
3. Sélectionne le dossier `BrainOS` que tu as préparé à l'étape 1
4. Valide

Tu vois maintenant la structure de BrainOS dans Obsidian. Félicitations — tu as un Coffre (Vault) opérationnel.

---
## Étape 3 — Installer Node.js

Node.js est un petit programme que Claude Code utilise en coulisses.

1. Va sur [nodejs.org/download](https://nodejs.org/en/download)
2. **Ignore le gros bloc noir en haut de la page** (ce sont des commandes pour utilisateurs avancés, tu n'en as pas besoin)
3. Descends jusqu'à la section *"Or get a prebuilt Node.js®"*
4. Clique sur le bouton vert qui correspond à ton système :
   - **macOS Installer (.pkg)** si tu es sur Mac
   - **Windows Installer (.msi)** si tu es sur Windows
   - Pour Linux : choisis le paquet adapté à ta distribution
5. Un fichier se télécharge. Double-clique dessus pour lancer l'installeur
6. Clique **Suivant / Continuer** à toutes les étapes, accepte la licence, valide l'installation
7. Ferme l'installeur quand c'est terminé

---
## Étape 4 — Installer Visual Studio Code

1. Va sur [code.visualstudio.com](https://code.visualstudio.com)
2. Télécharge la version pour ton système
3. Installe-la

---
## Étape 5 — Ouvrir ton BrainOS dans Visual Studio Code

1. Lance VS Code
2. Menu **File → Open Folder…** (Mac : `Fichier → Ouvrir le dossier…`)
3. Sélectionne ton dossier `BrainOS`
4. Valide

Tu vois maintenant les mêmes fichiers que dans ton Finder/Explorateur et dans Obsidian, mais côté technique. Tu vois même un dossier .claude qui n'est pas visible ailleurs.

---
## Étape 6 — Ouvrir le terminal intégré

Un "terminal" est une petite fenêtre où tu tapes des commandes. 
Nous l'utiliserons dans un premier temps pour vérifier l'installation de Node.js, puis pour installer le CLI de Claude Code (qui est différent de l'app native Mac/Windows de Claude.)

Dans VS Code, menu **Terminal → New Terminal**.

Une zone noire ou foncée s'ouvre en bas de ta fenêtre. C'est ton terminal. Laisse-le ouvert, on va l'utiliser dans les étapes suivantes.

---
## Étape 7 — Vérifier que Node.js est installé

Dans le terminal de VS Code, tape exactement :

```
node --version
```

Puis appuie sur **Entrée**.

Tu dois voir une ligne qui ressemble à `v20.11.0` (peu importe le numéro, du moment qu'il commence par `v18` ou plus).

Si tu vois un message d'erreur du genre *"command not found"*, redémarre VS Code et réessaye.

---

## Étape 8 — Installer Claude Code

Dans le même terminal, tape cette commande :

```
npm install -g @anthropic-ai/claude-code
```

Et appuie sur **Entrée**.

Ça va installer Claude Code sur ton ordinateur. Ça prend entre 30 secondes et 2 minutes.
⚠️ **Mac uniquement** : si tu vois une erreur de permission, tape plutôt :

> ```
> sudo npm install -g @anthropic-ai/claude-code
> ```

C'est une commande Admin pour dire que tu es admin et que tu forces l'installation. Le terminal te demandera le mot de passe de ton Ordinateur (mot de passe Mac ou Windows). Tu vas l'écrire, mais il ne s'affichera pas par sécurité, c'est normal puis appuie sur **Entrée**.

### Première connexion

Une fois Claude installé, toujours dans le terminal, tape simplement :

```
claude
```

Appuie sur **Entrée**. Une page web va s'ouvrir dans ton navigateur pour te connecter à ton compte Claude. Suis les instructions, autorise, ferme l'onglet. Tu es connecté.

De retour dans le terminal, Claude Code est prêt.

---

## Étape 9 — Installation du plugin Claude Code for VS Code

Dans Visual Studio Code, à gauche de ton écran, tu as accès à plusieurs icônes.
Les 4 pièces de puzzle sont les extensions.

Clique dessus et cherche Claude.
Installe l'extension d'Anthropic "Claude Code for VS Code".
Active-la si nécessaire.

Une fois installé, le logo de Claude apparaîtra à gauche sous les 4 pièces de puzzle.
Clique dessus et connecte-toi à ton compte Claude (une fenêtre du navigateur devrait s'ouvrir).
Une fois connecté, retourne dans Visual Studio Code, dans l'extension Claude et tu devrais voir un bouton en haut "New session". Clique dessus.


Parfait, on peut commencer une session.

---

## Ton prochain pas

→ **[02-configure-your-brain.md](02-configure-your-brain.md)** — on configure ton BrainOS via une conversation avec Claude.
