
# Composants input for React

## Prérequis

- `node.js` > v16
- `Git`

- Création de votre projet React

```bash
npx create-react-app nom_du_projet
```

supprimer ensuite le contenu du dossier `src`

- S'assurer d'avoir un compte `npm` et d'y être logué sur le terminal. Dans le package.json, la partie `"private":true`  doit être supprimé.

```bash
# savoir si on est connecté
npm whoami
# Se connecté à npm à partir du terminal 
npm login
```

## Architecture

Dans le dossier `src`, placer un dossier `lib`
Il va contenir tous les composants et styles nécessaire au module.
il faut ajouter aussi un fichier `index.js` qui regroupera tout les fichiers des composants.
---

Exemple :
|Niveau|---|---|---|
|---|---|---|---|
|0 Racine|src|---|---|
|1|lib|---|---|
|2|components |css |index.js|
|3|Input.js / Modale.js|style.css||

Dans le fichier index, on regroupe les composants Modale et input et on les partages.

```javascript
// src/lib/index.js
import Modale from "./components/Modale";
import Input from "./components/Input";
export {Modale,Input};
```

---

## Procédure de publication

- [Doc npm](https://docs.npmjs.com/getting-started/publishing-npm-packages)

### Configuration

- Avant de publier votre package, placer votre nom d'utilisateur ou pseudo devant la propriété name du package.json pour s'assurer d'avoir un module avec un nom unique. Déplacé les scripts de
`dependencies` dans `devDependencies`, et copier dans `peerDependencies` les scripts de React et react dom.
De plus, modifier le script build.

```json
// Nom du projet
"name": "@john_doe/nom_du_projet",
"description": "Ce que fait le super projet en cours"
// point d'entrée du nom_du_projet
"main":"dist/index.js",
"files":["dist", "README.md"], 
"module":"dist/index.js"
// Les fichiers a publier
"scripts": {
    "build": "rm -rf dist && NODE_ENV=production babel src/lib --out-dir dist --copy-files --ignore __tests__,spec.js,test.js,__snapshots__",  
}
"devDependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  },
  "peerDependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  }
```

- Installer [le babel cli](https://babeljs.io/docs/usage/cli/)

Puis à la racine du projet, créer un fichier `.babelrc` avec les instructions ci-dessous.

```json
{  
    "presets":
     [["react-app", { "absoluteRuntime": false }]]
}
```

On s'assure d'avoir un nom unique pour son module :

```bash
# exemple :
npm search nom_du_projet
```

## Publication

Lancer la commande :

```bash
npm run build
```

Un dossier `dist` doit être créé à la racine.

Création du Package :

```bash
# commande pour un package payant / private
npm publish
# ou
# commande pour un package gratuit / public *recommandé
npm publish --access public
```

## Patch

- En cas de correction du package ou du code, si on utilise git, faire un commit puis mettre a jour son numero de version avec la commande ci-dessous :

```bash
git add .
git commit -m "Mise à jour de mon package"
git push
# indique le nouveau numéro de version (incrémente automatiquement le semver)
npm version patch 
# run est optionnel dans ce cas
npm publish --access-public
```

## Installation sur un projet

Installation de la librairie

```bash
npm install nom_du_projet
```

```javascript
// React
import { MonCompo } from "nom_du_projet"
```
