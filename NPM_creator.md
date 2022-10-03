
# Composants input for React

## Prérequis

- `node.js` > v16
- `Git`

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
|Architecture|---|---|
|---|---|---|
|src|---|---|
|lib|---|---|
|components |css |index.js|
|Modale.js| Input.js|---|

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

- Avant de publier votre package, placer votre nom d'utilisateur ou pseudo devant la propriété name du package.json pour s'assurer d'avoir un module avec un nom unique.

Ainsi que de modifier le script build.

```json
"name": "john_doe/nom_du_projet",
// Les fichiers a publier
"files":["lib/**/*"], 
// plus bas 
"scripts": {
    "build": "rm -rf dist && NODE_ENV=production babel src/lib --out-dir dist --copy-files --ignore __tests__,spec.js,test.js,__snapshots__",  
}
```

On s'assure d'avoir un nom unique pour son module :

```bash
# exemple :
npm search react
```

Création du Package :

```bash
npm run publish
# ou
npm run publish --access-public
```

- En cas de correction du package, si on utilise git, mettre à jour son dépôt avant de publier :

```bash
npm version patch 
# indique le nouveau numéro de version
npm publish --access-public
# run est optionnel dans ce cas
```

Installation de la librairie

```bash
npm install nom_du_projet
```
