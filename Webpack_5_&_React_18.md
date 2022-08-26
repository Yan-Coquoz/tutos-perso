# Starter React

React 18 et Webpack 5 babel prettier eslint sass

## initalisation du projet

```bash
npm init
# et
git init
```

## Organisation

- Créer un dossier `public` et un dossier `src`.
- Mettre dans le `public` un fichier `index.html`.
- A la racine du projet mettre un fichier `.gitignore` en excluant les dossiers `node_modules` et `dist`.

Contenu du fichier index.html:

```html
<!DOCTYPE html>
<html lang="fr">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Starter React</title>
</head>

<body>
    <div id="root"></div>
    <script src="../dist/bundle.js"></script>
</body>

</html>
```

## Installation de babel

```bash
npm install --save-dev @babel/preset-react @babel/core @babel/cli @babel/preset-env
```

Babel est un transpilateur, il permet de convertir le `jsx` en javascript lisible pour le navigateur.

Pour la configuration de Babel, créer un fichier `.babelrc` à la racine du projet:

```json
{
  "presets": ["@babel/env", "@babel/preset-react"]
}
```

Les différents plugins disponible [sur le site](https://babeljs.io/docs/en/plugins/)

## Installation de Webpack

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server style-loader babel-loader
```

- [l'api de Webpack](https://webpack.js.org/api/webpack-dev-server/#installation)
- [Gestion des styles](https://webpack.js.org/loaders/style-loader/#root)
- [Babel Loader](https://webpack.js.org/loaders/babel-loader/)
- [Utilisation du CSS](https://webpack.js.org/loaders/css-loader/)
- [Utilisation du SCSS](https://webpack.js.org/loaders/sass-loader/) A la place du CSS.

### Configuration de Webpack

Création d'un dossier `config` à la racine du projet, d'un fichier de configuration `webpack.config.js` ainsi que d'un fichier pour les routes à suivre `paths.js`.

```javascript
const path = require("path");

module.exports = {
  src: path.resolve(__dirname, "../src"), //source files
  assets: path.resolve(__dirname, "../src/assets"),
  builds: path.resolve(__dirname, "../dist"), // production
  static: path.resolve(__dirname, "../public"),
};
```

```javascript
// webpack.config.js
const paths = require("./paths");
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");

const port = 3000;

module.exports = {
  entry: [paths.src + "/index.js"],
  devtool: "source-map",
  optimization: {
    usedExports: true,
  },
  output: {
    path: paths.build,
    publicPath: "/",
    filename: "js/[name].[contenthash].js",
    clean: true,
  },

  resolve: {
    extensions: ["*", ".js", ".jsx"],
    alias: {
      src: paths.src,
      app: paths.src,
    },
  },

  plugins: [
    new HtmlWebpackPlugin({
      favicon: paths.assets + "/favicon.ico",
      template: paths.assets + "/index.html",
    }),
  ],

  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: "babel-loader",
        options: { presets: ["@babel/env"] },
      },
      {
        // CSS
        test: /\.(s?css)$/,
        use: ["style-loader", "css-loader", "sass-loader"],
      },
      {
        // images
        test: /\.(ico|gif|png|jpe?g|webp|svg)$/i,
        use: [
          {
            loader: "file-loader",
          },
        ],
      },
      {
        // Fonts
        test: /\.(woff2?|eot|ttf|otf)$/,
        use: [
          {
            loader: "file-loader",
          },
        ],
      },
    ],
  },

  devServer: {
    static: {
      directory: paths.static,
      publicPath: "http://localhost:3000/dist/",
    },
    historyApiFallback: true,
    compress: true,
    port,
    hot: true,
    open: true,
    client: {
      overlay: true,
    },
  },
};
```

Explications sommaire :

- `entry` est le point d'entrée de notre application pour Webpack et lui indique aussi ou sont regroupés nos fichiers.
- `module` aide a définir comment les modules exportés sont transforméset lesquel sont inclus en fonction du tableau `rules`.

Notre première règle consiste à transformer notre syntaxe ES6 et JSX. Les propriétés `test` et `exclude` sont des conditions avec lesquelles faire correspondre le fichier. Dans ce cas, il correspondra à tout ce qui se trouve en dehors des répertoires `node_modules` et `bower_components`. Puisque nous allons également transformer nos fichiers `.jset` et `.jsx`, nous devrons demander à Webpack d'utiliser Babel. Enfin, nous précisons que nous voulons utiliser le `env` préréglage dans [les options](https://webpack.js.org/configuration/module/#rule-options-rule-query).

La règle suivante concerne le traitement du CSS. Puisque nous ne pré-ou post-traitons pas notre CSS, nous devons juste nous assurer d'ajouter `style-loader` et `css-loader` à la  propriété `use`. `css-loader` a besoin de `style-loader` pour travailler. `loader` est un raccourci pour la propriété `use`, lorsqu'un seul chargeur est utilisé.

La propriété [`resolve`](https://webpack.js.org/configuration/resolve/) nous permet de spécifier les extensions que Webpack résoudra — cela nous permet d'importer des modules sans avoir besoin d'ajouter leurs extensions.

La propriété [`output`](https://webpack.js.org/configuration/output/) indique à Webpack où placer notre code groupé. La propriété [`publicPath`](https://webpack.js.org/configuration/output/#output-publicpath) spécifie dans quel répertoire le bundle doit aller et indique également à `webpack-dev-server` d'où servir les fichiers.

La propriété `publicPath` est une propriété spéciale qui nous aide avec notre serveur de développement. Il spécifie l'URL publique du répertoire - du moins pour autant que `webpack-dev-server` nous sachions ou nous en soucions. S'il n'est pas défini correctement, vous obtiendrez des 404 car le serveur ne servira pas vos fichiers à partir du bon emplacement !

Nous nous sommes installés [`webpack-dev-server`](https://webpack.js.org/configuration/dev-server/) dans la propriété `devServer`. Cela ne nécessite pas grand-chose pour nos besoins - juste l'emplacement à partir duquel nous servons les fichiers statiques (tels que notre index.html) et le port sur lequel nous voulons exécuter le serveur. Notez que `devServer` possède également une propriété [`publicPath`](https://webpack.js.org/configuration/dev-server/#devserver-publicpath-). Cela indique `publicPath` au serveur où se trouve réellement notre code groupé.

Ce dernier élément aurait pu être un peu déroutant - Faites très attention ici : [`output.publicPath`](https://webpack.js.org/configuration/output/#output-publicpath) et [`devServer.publicPath`](https://webpack.js.org/configuration/dev-server/#devserver-publicpath-) sont différents.

Enfin, puisque nous voulons utiliser le `hotModuleReplacement`, nous n'avons pas besoin d'actualiser constamment pour voir nos modifications. Tout ce que nous faisons pour cela en termes de ce fichier est d'instancier une nouvelle instance du plugin dans la propriété `plugins` et de nous assurer que nous définissons `hot` sur `true` dans `devServer`.
[hot module Doc](https://webpack.js.org/guides/hot-module-replacement/)

- Installation de `fileLoader` qui permet de charger les images.

```bash
npm install file-loader --save-dev
```

Configuration du module dans le fichier `webpack.config.js`:
[file loader](https://v4.webpack.js.org/loaders/file-loader/#getting-started)

## installation de React

```bash
npm install react react-dom
```

### Mise en place

Dans le dossier `src`, créer un fichier `index.js` c'est le point d'entrée de l'application.

```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App.js";

ReactDOM.render(<App />, document.getElementById("root"));
```

Toujours dans `src`, créer un dossier `componants` et un fichier `App.js`.

```javascript
import React from "react";

import "./app.scss";

const App = () => {
  return (
    <div className="app">
      <h1>Hello you</h1>
    </div>
  );
};

export default App;
```

## installation de Prettier et eslint

### configuration

## installation  React Router
