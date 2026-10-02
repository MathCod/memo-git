# Fiche de réponses : piloter GitHub depuis le terminal avec GitHub CLI

Nom et prénom : BERGER Mathias

Compte GitHub : MathCod

Adresse du dépôt créé pendant le TP : https://github.com/MathCod/tp-gh-cli.git

Système d'exploitation et terminal utilisés : Windows/GitBash

On répond à chaque question au moment où le document de TP l'indique. Quand une question demande de copier un résultat de commande, on le colle dans un bloc de code.

À la fin de chaque partie, on indique les difficultés rencontrées : commande qui a échoué, message d'erreur, consigne mal comprise. S'il n'y en a pas eu, on écrit « Aucune ».

La fiche est individuelle.

## Partie 1 : vérifier l'installation et se connecter

### Q1 (section 1.2)

a) Copier le résultat de `gh --version` et celui de `gh auth status`. On copie le résultat tel qu'il s'affiche, avec le jeton masqué par des astérisques.

$ gh --version
gh version 2.102.0 (2026-09-30)
https://github.com/cli/cli/releases/tag/v2.102.0

$ gh auth status
github.com
  ✓ Logged in to github.com account MathCod (keyring)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'

b) D'après `gh auth status`, quel protocole est utilisé pour les opérations Git ? Quelles autorisations la ligne `Token scopes` liste-t-elle ?

Réponse : Le protocole utilisé est https.
Token scopes liste les autorisations qu'a CLI : 'gist', 'read:org', 'repo', 'workflow'

Difficultés rencontrées dans la partie 1 : Aucunes

## Partie 2 : créer un dépôt et l'explorer

### Q2 (section 2.1)

a) Copier les lignes affichées par `gh repo create`.

$ gh repo create tp-gh-cli --public --description "Terrain d'essai pour GitHub CLI" --add-readme --clone
✓ Created repository MathCod/tp-gh-cli on github.com
  https://github.com/MathCod/tp-gh-cli
Cloning into 'tp-gh-cli'...

b) Sans GitHub CLI, quelles étapes aurait-il fallu enchaîner, dans l'interface web de GitHub puis dans le terminal, pour obtenir le même résultat ?

Réponse :

1. créer un repo sur Github
2. créer un dossier projets en local ("mkdir tp-gh-cli" puis 'cd tp-gh-cli" pour entrer dedans)
3. dans le terminal enchainer les commandes :
git init
touch README.md
git add .
git branch -M main
git remote add origin https://github.com/MathCod/tp-gh-cli.git
git commit -m "initialisation du projet"
git push -u origin main

### Q3 (section 2.2)

a) Copier le résultat de `git remote -v`. Sous quel nom le dépôt GitHub est-il déclaré, et avec quel protocole ? À quel moment du TP ce protocole a-t-il été choisi ?

$ git remote -v
origin  https://github.com/MathCod/tp-gh-cli.git (fetch)
origin  https://github.com/MathCod/tp-gh-cli.git (push)

Le nom est "tp-gh-cli" avec le protocole https, le protocole a été choisis lors le l'authentification à CLI après l'installation.

b) Copier le résultat de `git log --oneline`. On n'a lancé aucune commande `git commit` : d'où vient ce commit ?

Réponse :

$ git log --oneline
1edf143 (HEAD -> main, origin/main, origin/HEAD) Initial commit

ce commit as été généré lors de la commande "gh repo create", il doit etre automatique

Difficultés rencontrées dans la partie 2 : Aucunes

## Partie 3 : gérer une issue

### Q4 (section 3.2)

a) Copier le résultat de `gh issue list`. Quelle information chaque colonne donne-t-elle ?

$ gh issue list

Showing 1 of 1 open issue in MathCod/tp-gh-cli

ID  TITLE                LABELS         UPDATED               
#1  Compléter le README  documentation  less than a minute ago

ID : numéro de l'issue
Labels : le label de l'issue
Updated : dernière modification


b) Que désigne la valeur `@me` passée à l'option `--assignee` ? Quel avantage a-t-elle par rapport au nom du compte écrit en toutes lettres ?

Réponse :

le `@me` désigne le compte connecté

Difficultés rencontrées dans la partie 3 : aucunes

## Partie 4 : ouvrir et fusionner une pull request

### Q5 (section 4.2)

a) Copier l'adresse affichée par `gh pr create`. Quel numéro la pull request porte-t-elle ? Pourquoi ne porte-t-elle pas le numéro 1, alors que c'est la première pull request du dépôt ?

https://github.com/MathCod/tp-gh-cli/pull/2

les Pull Requests partagent exactement le même compteur de numérotation que les issues

b) Que va produire la mention `Closes #1` au moment de la fusion ?

Réponse : 

`Closes #1` va fermer automatiquement l'issue

### Q6 (section 4.3)

Copier les lignes affichées par `gh pr merge --squash --delete-branch`. Lister les actions que la commande a réalisées, en précisant pour chacune si elle a eu lieu sur GitHub ou dans le dépôt local.

Réponse :

$ gh pr merge --squash --delete-branch
✓ Squashed and merged pull request MathCod/tp-gh-cli#2 (docs: lister les commandes gh dans le README)
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 2 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1014 bytes | 253.00 KiB/s, done.
From https://github.com/MathCod/tp-gh-cli
 * branch            main       -> FETCH_HEAD
   1edf143..e58a794  main       -> origin/main
Updating 1edf143..e58a794
Fast-forward
 README.md | 7 +++++++
 1 file changed, 7 insertions(+)
✓ Deleted local branch docs/1-completer-readme and switched to branch main
✓ Deleted remote branch docs/1-completer-readme

1. Fusion "Squash and merge" sur github
2. mise à jour de la branche main en local
3. Bascule de branche (switch/checkout) vers main en local
4. Suppression de la branche de travail "docs/1-completer-readme" en local
5. Suppression de la branche "docs/1-completer-readme" sur github

### Q7 (section 4.4)

a) Copier le résultat de `git log --oneline`. Combien de commits la branche `main` contient-elle ? Quel est le message du dernier, et d'où vient le numéro placé entre parenthèses à la fin ?

$ git log --oneline
e58a794 (HEAD -> main, origin/main, origin/HEAD) docs: lister les commandes gh dans le README (#2)
1edf143 Initial commit

1. La branche main contient 2 commits (le commit initial "1edf143" et le commit de fusion "e58a794")
2. Le message du dernier est : "docs: lister les commandes gh dans le README (#2)"
3. Le numéro viens de l'opération Squash and merge. Ce numéro correspond au numéro de la "Pull Request" qui a servi à intégrer ces modifications dans la branche principale.

b) D'après `gh issue view 1`, dans quel état se trouve l'issue #1 ? On n'a lancé aucune commande pour la fermer : expliquer ce qui s'est passé.

Réponse : l'issue #1 as été fermée automatiquement par la mention `Closes #1`

Difficultés rencontrées dans la partie 4 : Aucune

## Partie 5 : modifier le dépôt et chercher dans l'aide

### Q8 (section 5.2)

Compléter le tableau en cherchant dans l'aide de GitHub CLI. On n'exécute pas ces commandes.

| Besoin | Commande |
| --- | --- |
| Cloner le dépôt `Hello-World` du compte `octocat` |gh repo clone octocat/Hello-World|
| Renommer le dépôt courant en `bac-a-sable` |gh repo clone octocat/Hello-World|
| Lister uniquement les issues fermées du dépôt courant |gh issue list --state closed|
| Ouvrir la pull request numéro 2 dans le navigateur |gh pr view 2 --web|

### Q9 (section 5.3)

a) Pour chacune des actions suivantes, indiquer si on la réalise avec `git` ou avec `gh`, et justifier en une phrase la règle qui permet de trancher.

| Action | Outil |
| --- | --- |
| Créer une branche |git (ex. git switch -c <branche>)|
| Créer un dépôt sur GitHub |gh (ex. gh repo create)|
| Enregistrer une modification dans l'historique |git (ex. git commit)|
| Envoyer une branche sur le dépôt distant |git (ex. git push)|
| Ouvrir une pull request |gh (ex. gh pr create)|
| Commenter une issue |gh (ex. gh issue comment)|

b) Citer une situation où GitHub CLI fait gagner du temps par rapport à l'interface web, et une situation où l'interface web reste préférable.

Réponse :
GitHub CLI fait gagner du temps pour créer et envoyer un nouveau dossier sur github.
l'interface web reste préférable pour effectuer une revue de code (Code Review).

Difficultés rencontrées dans la partie 5 : Aucune
