# Les test avec React, Jest et Enzyme

## Configuration dans le projet

[Jest](https://jestjs.io/docs/tutorial-react)
[Enzyme](https://www.npmjs.com/package/enzyme)

- Installation de `jest`

```bash
yarn add --dev jest babel-jest @babel/preset-env @babel/preset-react react-test-renderer
```

ou avec le modele fournit par la formation

```bash
yarn add --dev jest babel-jest react-test-renderer
```

- Installation de `enzyme`

```bash
yarn add --dev enzyme enzyme-adapter-react-16
```

## Configuration du package.json

Ajouter ses lignes:
en fin de page

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
     "<rootDiv>/tests/.setup.js"
   ]
 }
```

explications :

---

- `<rootDir>/src` c'est la racine du projet et le chemin des fichier à tester.
- `<rootDir>/tests` c'est la racine du projet et le dossier des tests.
- `moduleNameMapper` ce qu'il y a là, se sont les extensions de fichier à simuler pour eviter les problemes pour les tests avec leurs emplacements.
- `setupFilesAfterEnv` configuration d'Enzyme et son emplacement

puis au niveau des scripts dans ce même fichier, ce qui dit que `jest` sera lancé depuis cette emplacement

```json
 "test": "jest"
```

ou bien si on des problèmes

```json
"test": "cross-env NODE_PATH=./ jest"
```

## Création de dossiers

- A la racine du projet, un dossier `tests` puis un dossier `__mocks__`.
- Dans le 1er dossier :
  1. un fichier `.setup` destiné à `enzyme`

```javascript
const enzyme = require("enzyme");
const Adapter = require("enzyme-adapter-react-16");
enzyme.configure({ adapter: new Adapter() });
```

  2. un fichier `.eslintrc` pour `jest`

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

## explications

- `jest/globals` => dit que Jest est valable de partout
- `no-unused-expressions` => il est dit ici que les constantes `const` on le droit de ne pas êtres assigné

- Dans le dossier `__mocks__`
  un fichier `fileMocks.js` et `styleMocks.js`
  Le 1er est destiné aux fichiers de medias (images, videos, musiques) et le second aux styles (css, scss, less).
  Ce qui correspond à la partie `moduleNameMapper` du package.json

  Dans ce 1er fichier :

```javascript
module.exports = "test-file-stub";
```

et dans le second un objet vide

```javascript
module.exports = {};
```

Placer le dossier `tests` et `__mocks__` dans le fichier `.gitignore`

- Fin de la config. -

---
