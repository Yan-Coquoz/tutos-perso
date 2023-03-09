# Création du dark mode.

Pour la facilité la lecture du fichier avec VSCode : `ctrl+k` puis `v`.

Une petite astuce pour créé le dark mode à partir d'un lien des favoris du navigateur.

La manipulation est faite sous chrome pour ma part, mais rien n’empêche de le faire avec un autre navigateur.

- Faire un clique droit au niveau de la barre des favoris. Un menu apparaît. Sélectionner le gestionnaire de favoris.
- Vous vous retrouver avec une page affichant l'organisation de vos favoris.
- En haut et à droite de votre navigateur, il y a un menu. Sélectionner Ajouter un favoris.
- Une petite modale apparaît. Donner lui le `Nom` que vous souhaiter (ex: mode nuit).
- Puis pour l'`URL`, renter le code JS en format texte qui suit :

```text
javascript: function addcss(css){      var head = document.getElementsByTagName('head')[0];      var s = document.createElement('style');      s.setAttribute('type', 'text/css');      s.appendChild(document.createTextNode(css));      head.appendChild(s);  }  addcss("html{filter: invert(1) hue-rotate(180deg)}");  addcss("img{filter: invert(1) hue-rotate(180deg)}");  addcss("video{filter: invert(1) hue-rotate(180deg)}");
```

- Enfin cliquer sur le bouton `enregistrer`.

Aller sur un site qui ne possède pas de mode nuit et cliqué sur le lien nouvellement créé.
