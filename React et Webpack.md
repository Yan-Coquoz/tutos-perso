
# Instalation React (lourde)

[La Docs de React](https://fr.reactjs.org/docs/create-a-new-react-app.html)

## Dans le dossier de votre app

- npx create-react-app mon-app
- cd mon-app
- npm start

# Instalation React Custum (little)

## Création d'un dossier pour votre nouveau project Réact

### 1 Création des dossiers initiaux

- `Mon-Project`
- `Mon-Project/dist`
- `Mon-Project/src`

### 2 Création des fichiers de base

- `.gitignore`
- `dist/index.html`
- `src/index.js`

### 3 Intégration dans les fichiers

- `.gitignore`
  
```shell
    .node_modules/
```

- `dist/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <script src="./main.js" async></script>
</head>
<body>
  <h1>Webpack</h1>
</body>
</html>
```

- `src/index.js`

```js
    console.log('hello');

    const sum = (a, b) => a + b;
```

## Commande dans le terminal

- Pour initialer le project

  - `yarn init` plus rapidement `yarn init -y`
  - `npm init`  plus rapidement `npm init -y`

- Pour initialer le project sur `git`
  
    `git init`

---

## Instalation des Outils

### WebPack

- Pour lancement de webpack faire les commandes suivante:

```bash
yarn add webpack-cli --dev
./node_modules/.bin/webpack
./node_modules/.bin/webpack --mode=production
./node_modules/.bin/webpack --mode=development
```

Suite à ses commande, webpack à creer un fichier  `./dist/main.js`

---

- Creation de nos racoursie dans `package.json`

```json
  "scripts": {
    "build:dev": "./node_modules/.bin/webpack --mode=development",
    "build": "./node_modules/.bin/webpack --mode=production"
  },
```

ou

```json
  "scripts": {
    "build:dev": "webpack --mode=development",
    "build": "webpack --mode=production"
  },
```

- Au final :

```json
{
  "name": "react",
  "version": "1.0.0",
  "description": "les outils de base",
  "main": "index.js",
  "license": "MIT",

  "scripts": {
    "build:dev": "webpack --mode=development",
    "build": "webpack --mode=production"
  },

  "devDependencies": {
    "webpack": "^5.24.3",
    "webpack-cli": "^4.5.0"
  }
}
```

- Pour pouvoir taper ses commandes plus vite dans le terminal

```js
yarn build:dev
yarn build
```

---

### Babel

installation de babel

```bash
yarn add --dev @babel/core @babel/preset-env @babel/preset-react babel-loader

npm i --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
```

configuration de babel de `es6` a `es5`

création du fichier de configuration de babel a la racine de notre project

`.babelrc`

et à l'intérieure de ce fichier

```js
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

cretion du fichier de configuration de webpack à la racine du project

`webpack.config.js`

 et a l'intérieure du fichier

```js
module.exports = {
  mode: 'development',
  module: {
    rules: [{
      test: /\.js$/,
      use: 'babel-loader'
    }]
  }
};
```

## webpack-dev-serveur

le WebPack serveur c'est le nodemon de Réact

installation dans le terminal

```bash
  yarn add --dev webpack-dev-server

  npm i --save-dev webpack-dev-server
```

creation du racourcie

`"start": "webpack serve"`

pour le lancer dans le terminal

start dans `package.json`

```json
{
  "name": "outils",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "build:dev": "webpack",
    "build": "webpack --mode=production",

    "start": "webpack serve"

  },
  "devDependencies": {
    "@babel/core": "^7.13.8",
    "@babel/preset-env": "^7.13.9",
    "@babel/preset-react": "^7.12.13",
    "babel-loader": "^8.2.2",
    "webpack": "^5.24.3",
    "webpack-cli": "^4.5.0",
    "webpack-dev-server": "^3.11.2"
  }
}
```

pour se lancer dans le bon dossier `dist`
avec config du bon dossier du port et ouvre une page web sur le port

```js
dans webpack.config.json
module.exports = {
  mode: 'development',
  module: {
    rules: [{
      test: /\.js$/,
      use: 'babel-loader'
    }]
  },

  devServer: {
    contentBase: 'dist',
    port: 3000,
    open: true
  }

};
```

pour le lancer dans le terminal

`yarn start`

pour le fermer `ctrl + c`

---

Pour augmanter le nombre page a regarder dans un terminal

```bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```
