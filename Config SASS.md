# SASS

## Configuration SASS

mettre SASS en global si ce n'est déja fait.
`-g` : installe le package en global, sur la machine.

````bash
  npm -g sass
````

Puis le dans le package.json.

- **Attention** à l'architecture des dossiers **et** au noms des fichiers

````json
{
  "scripts": {
    "sass": "sass --watch ./sass/main.scss:./public/style.css --style compressed"
  }
}

````

- `sass` : ce que l'on va utiliser.
- `--watch` : permet de relancé le serveur, de rafraichir la page en direct. peut être remplacé par `-w`.
- `--style compressed` La façon dont le fichier css sera rendu grâce au flag `--style`.
  *Les options possibles :*
  1) `Nested` : imite le nesting SASS tout en maintenant une syntaxe CSS correcte.
  2) `Expended` : Le plus proche de la façon dont on écris le CSS. (facile à lire).
  3) `Compact` : met le selecteur et son ensemble sur une seule ligne.
  4) `Compressed` : minifie le code, supprime tout les espaces.

Lancement de SASS dans le terminal :

````bash
 npm run sass
````

---
Pour le projet l'architecture de SASS ce fait en 7.1.
Liste des dossiers utilisés :

- base : Les fondation communes (la police, le box-sizing...).
- utils : Tout ce qui est variables, mixins, % placeholder, fonctions...
- layouts : Les blocs BEM réutilisable (header, footer formulaire, nav ...).
- components : Blocs BEM indépendant (bouton, icons...).
- pages : Tout ce qui est spécifique à une page.
- themes : tout ce qui touche à des themes spécifique (fête de noel, black friday...)
- vendors : Tous ce qui est externe au site, (bootstrap, Jquery UI...).

## Config compatibilité navigateurs

Installation d'autoprefixer, postcss, et postcss-cli

````bash
npm install autoprefixer postcss postcss-cli -g
````

Dans le package.json :

````json
{
  "scripts": {
  "prefix": "postcss ./public/style.css --use autoprefixer -d ./public/prefixed/"
},
"browserslist": "last 4 versions"
}
````

explications :

- On va utiliser la commande `npm run prefix`
- Qui va utiliser `postcss` sur le fichier `style.css` et qu'il va utiliser `autoprefixer` en mode developpement, et mettra le fichier à utilisé dans le dossier `prefixed`.
- La dernier ligne, est le rayon d'action d'autoprefixer, les 4 dernières versions des navigateurs.
