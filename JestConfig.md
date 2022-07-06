# Jest

Utilisation de Jest avec du **Javascript vanillia**.

- [Documentation de Jest](https://jestjs.io/fr/docs/getting-started)
- [Documentation  de Testing Library](https://testing-library.com/)

```bash
npm install -D babel-jest jest @babel/preset-env @testing-library/dom @testing-library/jest-dom @testing-library/user-event
```

- Jest DOM pour réaliser des tests d’intégration. Jest DOM permet de répliquer un DOM pour parcourir des pages et ajouter ou supprimer des `nœuds`.
- Testing Library est utilisée en complément des Jest DOM et facilite la sélection de `nœuds` [doc](https://testing-library.com/docs/dom-testing-library/intro/)

package.json

```json
{
    "scripts": {
    "test": "jest"
  },
}
```

A la suite de `jest` on peut ajouter `--coverage`, `--watch` ou `--watchAll` et d'autres options comme `--silent`, `--noStackTrace` [etc..](https://jestjs.io/fr/docs/cli#options).

- `--coverage` affiche un tableau de couverture de tous les fichiers couvert.
- `--watch` affiche un menu avec divers options :
  - exécuter tous les tests.
  - Les tests échoués.
  - Les tests avec les fichiers modifiés.
  - tests de fichiers avec regex.
  - test de pattern de regex.
  - quitté le menu de test.
  - relancé un tests
- `--watchAll` affiche un menu avec d'autres options :
  - Les tests échoués.
  - Les tests avec les fichiers modifiés.
  - tests de fichiers avec regex.
  - test de pattern de regex.
  - quitté le menu de test.
  - relancé un tests

Pour afficher toutes les option disponible avec Jest :

```bash
node_modules/.bin/jest --help
```

## Test de couverture

```Javascript
// Fichier à tester. hello.js
/**
 * @param {string} name 
 */
export const direBonjour = name => {
    if (!name) {
        return "Hello, World"
    }
    return `Hello, ${name}`
}
```

```Javascript
// fichier de test hello.test.js
import { direBonjour } from "./unit1";

describe("Hello test", () => {
  it('should return "Hello, World"', () => {
    expect(direBonjour()).toBe("Hello, World");
  });

  it('should be "Hello, Yan"', () => {
    expect(direBonjour("Yan")).toBe("Hello, Yan");
  });
});
```

Il y a 2 façons de lancer le script de test coverage :

```bash
# si l'option --coverage est dans le package.json
npm run test
# ou
node_modules/.bin/jest --coverage
```

Dans le tableau de couverture:

|File|% Stmts|% Branch|% Funcs| %Lines|uncovered Line #s|
|---|----|----|----|----|----|
|All files|100|100|100|100||
|hello.js|100|100|100|100||

`Stmts` (statements) est le taux de couverture.
`branch` Les instructions if dont les condtions ont été remplies au moins une fois par les tests unitaire.
`Funcs` (functions) Les fonctions ayant été appelées au moins une fois.
`Lines` les lignes de codes ayant été exécutées par les tests.
`uncovered Line` est la ou les lignes non couvertes par les tests présent.

Si je rajoute une condition et que je relance les tests, les valeurs du tabeau de couvertures auront changés et le numéro de ligne sera indiqué.

```javascript
// fichier de test hello.test.js
/**
 * @param {string} name
 */
export const sayHello = (name) => {
  if (!name) {
    return "Hello, World";
  }
  if (name === "Elise") {
    return "Hello Elise";
  }
  return `Hello, ${name}`;
};
```

|File|% Stmts|% Branch|% Funcs| %Lines|uncovered Line #s|
|---|----|----|----|----|----|
|All files|83.33|75|100|83.33||
|hello.js|83.33|75|100|83.33|9|

## Les tests les plus courant

- `Les tests unitaires` – ce sont souvent les premiers à être implémentés dans une base de code. On les ajoute à partir du moment où le produit a trouvé sa cible. Ils sont généralement “assez faciles” à réaliser.

- `Les tests fonctionnels` ou d’`intégration` – on les ajoute souvent soit en même temps que les tests unitaires, soit après. Ils vont être un peu plus complexes à réaliser.

- `Les tests E2E ou End 2 End` – ce sont des tests assez complexes, qui seront souvent réservés à la phase de maturité du projet.
