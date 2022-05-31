# A propos des formulaires

[mdn](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Mon_premier_formulaire_HTML)

Un formulaire est un ensemble de champs, cad de zones intéractives que l'utilisateur pourra compléter.

Un fois rempli ce formulaire pourra être validé, on dit soumis, pour traitement. Aujourd'hui on ne s'occupe pas du traitement, on le verra en S2 et en S3. Finalement un formulaire est un moyen pour intéragir (s2) et pour générer une requete http (s3)

Aujourd'hui ce qui nous intéresse c'est uniquement la création du formulaire en HTML pour la fond et en CSS pour la forme, on va créer l'interface.

Un formulaire est représenté par une balise

```html
<form>
    <!-- ici on mettra le contenu du form -->
</form>
```

Il pourra être configuré via les attributs classique (class, lang, id, title, ...)

On peut lui mettre 2 attributs propre aux formulaire

- action -> la destination, là où on sera diriger à l'envoi du formulaire
- method -> la manière dont les infos seront passées (on verra en s3)

## Quoi mettre dans le form ?

On va mettre des champs intéractifs, représentés par des balises, pour que l'utilisateur puisse saisir des infos

On met généralement des champs DANS un formulaire, ainsi à la soumission les valeurs des champs sont envoyées

### La balise `textarea`

Elle sert à délimiter une zone de saisi de texte long (sur plusieurs ligne)
Elle pourra être configurée via les attributs classique (class, lang, id, title, ... (d'ailleurs  toutes les balises qui suivent également))
Et aussi avec les attributs propre aux champs de formulaires :

- L'attribut `placeholder` : sert à mettre un texte d'aide à la saisi qui apparait quand le champ est vide
- L'attribut `name` : sert à étiqueter la valeur saisie par l'utilisateur à la soumission

### La balise `button`

Element cliquable qui va servir interagir pour déclencher une action

- L'attribut `type` sert à choisir le type d'action
  - La valeur `submit` (le type par défaut), au clic, le formulaire qui entoure le bouton sera envoyé avec toutes les valeurs des champs qu'il contient
  - La valeur `button`, au clic, on fait rien, ce sera au developpeur de dire ce que fait le bouton en javascript (s2)
  - La valeur `reset`, au clic, le formulaire sera vidé, mais rien ne sera envoyé

### La balise `label`

La balise label sert à étiqueter un champ, pour donner une info aux être humain qui utilise notre site

Une bonne pratique consite à associer dans le code nos label avec le champ correspondant, pour cela on a le choix entre 2 solutions :

1. On met le champ DANS le label

```html
<label>
    Message
    <textarea></textarea>
</label>
```

2. On met un attribut `for` sur le label correspondant à l'`id` du champ

```html
<label for="message">Message</label>

<textarea id="message"></textarea>
```

### La balise `input`

La balise input (autofermante) sert à mettre une zone de saisi, ce qu'on pourra saisir sera influencé par le type de l'input

- L'attribut `type`
  - `text` -> sert à saisir du texte court sur une ligne (si on fait entrée en ayant focus le formulaire est soumis)
  - `number` -> sert à faciliter la saisi d'un nombre
  - `password` -> les caractères seront cachés visuelement
  - `file` -> au clic on ouvrire un explorateur de fichier
  - `radio` -> case à choix unique, pour relier plusieurs input de type radio ensemble on leur met le même `name`
    - L'attribut `checked` sert à précocher un choix
  - `checkbox` -> case à choix multiple, fonctionne comme les radio sauf qu'on peut en cocher plusieurs
  - ... [mdn](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Input)
- On retrouve également l'attribut `placeholder` et `name`
- L'attribut `value` sert à ititialiser la valeur d'un champ

### La balise `fieldset`

Sert à délimiter un groupe de champs

### La balise `legend`

Sert à légender un fieldset

### La balise `select`

Champ pour choisir un choix parmis une liste de choix

- On retrouve l'attribut name propre aux champs
- On spécifie à l'intérieur tous les choix via des balises `option`

```html
<select name="level">
    <option value="bac">Bac</option>
    <option value="bac2">Bac +2</option>
    <option value="bac3">Bac +3</option>
    <option value="bac5">Bac +5</option>
</select>
```
