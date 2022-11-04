# Déploiement d'un projet React avec Github pages

## Créer votre application React

```bash
npx create-react-app mon_app
```

Créer votre votre repository sur GitHub, et lié l'application.

```bash
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:identifiant_github/mon_app.git
git push -u origin main
```

## package et config

Ajout de github pages dans le projet au niveau des dépendances de dev :

```bash
npm install gh-pages --save-dev
```

Dans le package.json, on ajoute quelques ligne :

```json
{
    "homepage": "https://identifiant_github.github.io/mon_app",
    "scripts":{
        "predeploy": "npm run build",
        "deploy": "gh-pages -d build"
    }
}
```

**Attention à la ligne de *homepage*, cette ligne est l'URL de la future application et respect une nomenclature interne à Github.**

## Déploiement

Une fois que l'app est pertinente au niveau de sa fonctionnalité on lance la commande de build de github

```bash
npm run deploy
```

- Cela doit créer un dossier build dans le projet à sa racine.
- Ensuite, on commit et on push.

```bash
git add .
git commit -m "First deploy"
git push
```

l'application est déployée.
