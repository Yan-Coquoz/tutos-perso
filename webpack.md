# Installation de Webpack

Pour lire ce fichier avec VSCode `ctrl + maj + v`

Webpack, nous permet de minifier notre code, de le packager, de le structurer, d'utiliser des bibliotheques grâce à la communauté, et de le transpiler, et d'avoir un serveur afin d'avoir un rendu apres chaque modification du code.

Avant toutes choses, **Nodejs** doit être installé.
Pour voir la version de Nodejs:

```bash
node --version
```

- Préparation d'un projet

  ```bash
  npm init
  ```

- installation de Webpack

  ```bash
  npm install webpack webpack-cli --save-dev
  ```

Webpack s'installe en mode dev avec la commande `--save-dev`

- ***Attention*** cette version de l'installation de Webpack est pour un simple projet html/css et js sans framework.

## Création d'un fichier de configuration de Webpack

À la racine du projet : `webpack.config.js`

- **Toutes les routes** dans ce fichier sont des routes qui partent de **la racine du projet** et ***non*** du fichier de configuration de webpack.

```javascript
const path = require('path');

module.exports = {
  mode: "production",
  entry: {
    app: "./src/index.js"
  },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve(__dirname, "dist")
  }
};
```

Explication de cette configuration :

En `production`, le point d'entrée de notre application sera `./src/index.js`.
Une fois compilé, il sera placé dans le dossier `./dist` avec pour nom de fichier `app.bundle.js`. `[name]` est une variable qui sera remplacée ici par `app`, car c'est ici ce qui désigne notre fichier de point d'entrée.

Pour lancé Webpack, il faut avant tout rajouté un script dans le package.json.

```json
"scripts": {
    "build": "webpack"
}
```

Une fois ce script placé, on peut lancé Webpack avec la commande :

```bash
npm run build
```

## Babel

   Pour s'assurer que notre code soit bien prit en charge par rapport aux évolution de JavaScript, il nous faut un transpilateur.
   Nous allons donc installer **Babel** et le **loader** de Webpack pour qu'ils puissent fonctionner ensemble.

- Les [plugin](https://webpack.js.org/plugins/) sont des options.
- les [loader](https://webpack.js.org/loaders/#transpiling) sont des package installer par le biais de npm / yarn ou autre.. Il faut bien penser à configurer à la suite de l'installation d'un package le fichier `webpack.config.js`.

```bash
npm install --save-dev babel-loader @babel/core @babel/preset-env babel-polyfill
```

- `babel-polyfill` permet de géré entre autre les promesses.
  Il est important de **le placé avant** l'appel de notre code dans la configuration de Webpack, pour s'assuer de la bonne prise en charge de notre fichier `index.js`.
- Configuration de babel dans le fichier de configuration de Webpack.

````javascript
const path = require('path');

const port = 3000;
module.exports = {
  mode: "production",
  entry: {
    polyfill: "babel-polyfill",
    app: "./src/index.js"
  },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve(__dirname, "dist"),
    clean:true,
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env"]
          }
        }
      }
    ]
  },
   devServer: {
    open: true,
    port,
  },
};
````

## Le serveur

Le serveur va nous permetre d'avoir un rendu côté navigateur après chaque modification de notre code.
Cette ligne de d'installation est variable seulement à partir de la version Webpack 5.

- [Configuration du serveur](https://github.com/webpack/webpack-dev-server) via Github

````bash
npm install -D webpack-dev-server
````

`-D` = est l'équivalent de `--save-dev`

A cette suite, il faut configuré le fichier package.json :

````json
 "scripts": {
    "start": "webpack serve --config ./config/webpack.config.js",
    "build": "webpack --config config/webpack.config.js",
    "clean": "rm -rf config/dist",
    "clean:all": "rm -rf config/dist node_modules package-lock.json",
     },
````

- Les scripts `clean` et `clean:all` permettre de repartir à zero pour le build ou bien pour réinstaller de nouvelles version des packages.

- Dans le fichier de configuration :

````javascript
  const webpack = require("webpack"); // permet de tenir compte du hot-reloading
  const port = 3000; // defini un autre port que le port 8080 

  module.exports = {

  devServer: {
    open: true, // ouvre le navigateur
    port,
    hot: true, // Permet le hot-reloading
  }

};

````

### Installation de plugin pour le HTML

   Ce plugin permet à webpack de savoir ou se situe le fichier HTML.

````bash
npm install --save-dev html-webpack-plugin
````

Dans le webpack.config.js :

````javascript
const path = require("path");
const webpack =require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");

const port = 3000;

module.exports = {
  mode: "production",
  entry: {
    polyfill: "babel-polyfill",
    app: "./src/index.js",
  },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: "gameon",
      filename: "./public/index.html",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env"],
          },
        },
      },
    ],
  },
  devServer: {
    open: true,
    port,
    hot:true,
  },
};

````

- [lien github](https://github.com/jantimon/html-webpack-plugin#options) pour la configuration du plugin
