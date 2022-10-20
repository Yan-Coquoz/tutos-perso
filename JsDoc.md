# Installation de la JSDOC

- [npm jsdoc](https://www.npmjs.com/package/jsdoc)
- [configuration de la JsDoc](https://jsdoc.app/about-configuring-jsdoc.html)

Si ce n'est déjà fait, il faut initialisé le projet.

````bash
npm init
# ou
npm init -y 
````

Ensuite installer le package de la **jsdoc**.

````bash
npm install -g jsdoc
# ou 
npm install -D jsdoc

````

Une fois installer ajouter un script au package.json.

````json
{
    "scripts": {
    "jsdoc": "jsdoc -c jsdoc.json"
  },
}
````

Cela permet de lancé le script et de le configuré grâce à la commande :

````bash
npm run jsdoc
````

Avant de lancé la commande, il faut créé un fichier jsdoc.json qui va contenir notre configuration.

````json
{
  "source": {
    "include": ["src"],
    "includePattern": ".js$",
    "excludePattern": "(node_modules/|docs/|public)"
  },
  "plugins": ["plugins/markdown"],
  "templates": {
    "cleverLinks": true,
    "monospaceLinks": true
  },
  "opts": {
    "recurse": true,
    "encoding":"utf8",
    "destination": "./docs/"
  }
}
````

### Petit plus

Extension VSCode :

- [VS DocBlocker](https://marketplace.visualstudio.com/items?itemName=jeremyljackson.vs-docblock)

Config complémentaire:

- Aller dans les paramètres de VSCode `ctrl + ,` dans la barre de recherche, tapé le mot `check` et s'assuré que les options sont bien cochées,

  - TypeScript › Check: Npm Is Installed

  - JS/TS › Implicit Project Config: Check JS

[voir plus de config](https://www.youtube.com/watch?v=h1nCs3tGpMM)
