# Cheat Sheet de Git

Configurer git :

```bash
git config --global user.name "Bozo Le Clown"
git config --global user.email "bozo.leclown@monemail.com"
git config --global core.editor code
git config --global color.ui true
```

```bash
# voir si tout c'est bien passé
git config -l 
```

Permet de push sur une nouvelle branche sans message d'erreur.

```bash
git config --global push.autoSetupRemote true
```

Initialisation d'un projet

```bash
git init
```

Copie un projet depuis un Repository (repo)

```bash
git clone adresseDuRepoDeGit
```

Connaitre le depot courant. Utiliser `-v` pour plus de précision.

```bash
git remote
git remote -v
```

Se connecter au repo distant.

```bash
git remote add upstream adressDuRepository
```

Etat du du dépot git sur notre hote

```bash
git status
```

Ajouter des fichiers ou un fichier en particulier.

```bash
git add . 
git add nomDuFichier
```

Supprimer un fichier du dépot git

```bash
git reset nomDuFichier
```

Faire un commit classique

```bash
git commit -m "Mon message"
```

Condense tous les fichiers suivis en les validant en une seule étape.

```bash
git commit -am "message du commit"
```

Modifier un commit avant qu'il soit push

```bash
git commit --amend -m "Mon nouveau message"
```

Liste toutes les branches. un * apparait sur la branche sur laquel on se trouve.

```bash
git branch
```

Création d'une nouvelle branche

```bash
git branch nomDeLaBranch
```

Changer de branche

```bash
git switch nomDeLAutreBranch
// ou
git checkout nomDeLAutreBranch
```

Changer de branche tout en créant une nouvelle branche

```bash
git checkout -b nouvelleBranche
```

Supprimer une branche. Se positionner sur une autre branche avant la suppression.

```bash
git branch -d nomDeLaBranch
```

Supprimer un dossier ou un fichier qui a été commit par erreur. ex: node_modules.
Après cette commande, **refaire** un commit et un push.

```bash
git rm --cache node_modules -r
```

Envois les commits sur les repo distant ( Avec `master` pour les anciens Repository )

```bash
git push origin main
git push origin master
```

Recupéré toutes les nouvelles infos du repo distant.

```bash
git pull
```

Fusionne les commits récupérés.

```bash
git merge upstream/main
```

Fusionne le commit d'une branche précise.( il faut se placé sur la branche de destination )

```bash
git merge nom_de_la_branche
```

**En cas de conflit après un merge, bien penser à refaire un commit**

Compare les fichiers modifiés qui se trouve dans la zone de transfert.

```bash
git diff --staged
```

Affiche les informations des commits, son historique.

```bash
git log
```

Affiche une representation graphique des commits.

```bash
git log --all --decorate --oneline --graph
```

Depuis un projet existant en Local, commande Git avec SSH :

```bash
git remote add origin git@github.com:Id_Github/Non_Du_Projet.git
git branch -M main
git push -u origin main
```

Création d'un repo en ligne de commande :

```bash

git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Id_Github/Non_Du_Projet.git
git push -u origin main
```
