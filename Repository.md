# Initialisation d'un fichier pour Github

---
**Windows**

1) Créez un dossier destiner à accueillir le projet.
2) Se placer à l'interieur.
3) Ouvrir le `terminal` (git bash)
4) Ecrire :

    ```bash
    git init
   ```

   Cette command initalise un projet avec git.

   ```bash
   code .
   ```

    Lance l'application `VSCode`.

---

**VsCode**

Créez les fichier dont vous avez besoin, metter en place votre base de code, votre architecture.
Une fois fait, ouvrez votre terminal `ctrl + ù`

```bash
git add .
git commit -m "votre message"
```

---

**Navigateur**

1) Allez dans votre compte Github, selectionnez l'onglet `Repository`
2) Cliquez sur le bouton *vert* : `new`.
3) Au niveau du champ de formulaire (Repository name) renter le nom de votre projet.
4) En dessous vous povez mettre une description du projet.
5) Selectionner public ou private selon le choix et l'inportance de votre projet. Je le conseil en public pour monter que vous êtes actif.
6) Vous pouvez dore et déjà créez votre projet en cliquant encore une fois sur le bouton *vert* : `Create repository`
7) Une fois fait , une page s'ouvre sur trois bloc avec des lignes de code. Selectionnez celui du milieu. Les lignes de code copier doivent être coller dans le terminal de VsCode.

```bash
git remote add origin [adresse Du Repository]
git branch -M main
git push -u origin main
```

A partir de là, votre projet qui est sur votre hôte (PC) est lier à github.

Continuer à taper votre vcode dans votre editeur. Après avoir sauvegarder et après être satisfait de votre travail, sauvegarder de nouveau votre code sur github. Je conseil de le faire à chaque petite étape.

**VsCode**

```bash
git add .
git commit -m "votre message de reussite"
git push
```
