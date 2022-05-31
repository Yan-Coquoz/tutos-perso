# Configuration de jest et Enzyme

- [Configuration de Jest avec React](https://jestjs.io/fr/docs/tutorial-react)
- [Config d'Enzyme](https://enzymejs.github.io/enzyme/docs/installation/)
- [Config de Jest avec Redux](https://redux.js.org/usage/writing-tests)

- _Configuration sans Create React App_ avec l'utilisation du model React avec Yarn.

```bash
yarn add --dev jest babel-jest @babel/preset-env @babel/preset-react react-test-renderer
```

- Avec le model O'clock, nous avons le `.babelrc` qui est similaire au `babel.config.js`

```json
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "useBuiltIns": "usage",
        "corejs": 3
      }
    ],
    "@babel/preset-react"
  ],
  "plugins": [
    "@babel/plugin-proposal-class-properties",
    "@babel/plugin-proposal-object-rest-spread"
  ]
}
```

- `"@babel/preset-env"` traduit de ES6 en ES5
- `"@babel/preset-react"` traduit de JSX en JS

Puis dans le _package.json_ on ajoute au scripts la commande de pour les tests :

```json
"scripts": {
    "test": "cross-env NODE_PATH=./ jest --watch --verbose"
  },
```

- `cross-env NODE_PATH=./` montre le chemin à executé.
- `--watch` lance un serveur comme _nodemon_, ce qui évite de lancé la commande de test à chaque fois.
- `--verbose` retourne plus d'explication lors du resultat du test.

- Toujours dans le package.json, on va configurer `Jest`

```json
"jest": {
    "roots": [
      "<rootDir>/src",
      "<rootDir>/tests"
    ],
    "moduleNameMapper": {
      "\\.(css|less|scss)$": "<rootDir>/__mocks__/styleMock.js",
      "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|mp4|avi|mkv|m4a|aac|oga)$": "<rootDir>/__mocks__/fileMock.js"
    },
    "setupFilesAfterEnv": [
      "<rootDir>/tests/.setup.js"
    ]
  }
```

- `<rootDir>` C'est la racine du projet, a partir d'ou Jest doit trouver les fichiers.
- `moduleNameMapper` tout ce qui concerne les styles, les images, les vidéos, les polices, et les fichiers son qui seront **mocké**.

- On crée donc ce fichier à la racine du projet : `__mocks__` et ses fichier `fileMock.js` `styleMock.js`

```javascript
// fileMock
module.export = "test-file-stub";
// on exporte juste une chaine de caractère
```

```javascript
// styleMock
module.export = {};
// on exporte juste un objet vide
```

- `setupFilesAfterEnv` A ce niveau, on configure un fichier `.setup.js` pour _Enzyme_ qui va nous aidé à la création d'un DOM virtuel. Il n'est pas obligatoire, il peut être remplacé par une autre librairie de React : `@testing-library/react` qui est installable avec cette commande :

```bash
  yarn add --dev enzyme enzyme-adapter-react-16
```

ou avec le npx create-react-app

```bash
  yarn add --dev @testing-library/react
```

- A la racine du projet, on créer un dossier `tests` puis on y place le fichier `.setup.js`

```javascript
// .setup.js
const { configure } = require("enzyme");
const Adapter = require("enzyme-adapter-react-16");
// A voir si la version de enzyme-adapter-react-16 est sorti

configure({ adapter: new Adapter() });
```

- Configuration d'eslint, on place dans le dossier `tests` un autre fichier `.eslintrc` qui viendra en complément du fichier du même nom qui est placé à la racine du projet dans le model React fourni par l'Ecole.

```json
{
  "env": {
    "jest/globals": true
  },
  "rules": {
    "no-unused-expressions": "off"
  }
}
```

Les tests à réalisés seront à mettre dans le dossier `tests` et dans un dossier du même nom que le fichier à tester.

le fichier à tester est par exemple `app.js`, le test se fera dans un fichier `app.test.js` ou `app.spec.js` dans un dossier se trouvant dans les dossiers `tests / App`
