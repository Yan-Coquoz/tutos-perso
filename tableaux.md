# Méthodes de tableau

## forEach

Méthode de tableau qui permet de **boucler** sur un tableau. Cette méthode prend un callback en argument. Ce callback sera appliqué sur chaque élément du tableau, il prend en paramètre l'élément courant, l'index courant et le tableau sur lequel on boucle.

```js
const monTableau = ['banane', 'poire', 'pomme'];
monTableau.forEach((elementCourant, indexCourant, tableau) => {
  console.log(`je mange : ${elementCourant}`);
  // en console ça donnera
  // 'je mange : banane'
  // 'je mange : poire'
  // 'je mange : pomme'
});
```

[Lien vers la doc MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

## map

Méthode de tableau qui permet de **transposer/transformer** un tableau originel en un nouveau tableau. Cette méthode prend en argument un callback qui sera appliqué sur chaque élément du tableau. Il prend en paramètre l'élément courant, l'index courant et le tableau sur lequel on boucle.

> Pour insérer une valeur transposée dans le nouveau tableau, il faut bien penser à `return` cette valeur dans le callback.

```js
const monTableau = ['banane', 'poire', 'pomme'];
const tableauTranpose = monTableau.map((elementCourant, indexCourant, tableau) => {
  return `je mange : ${elementCourant}`;
});
// tableauTranpose = ['je mange : banane', 'je mange : poire', 'je mange : pomme']
```

[Lien vers la doc MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

## filter

Méthode de tableau qui permet de **filter** un tableau originel en un nouveau tableau. Cette méthode prend en argument un callback qui sera appliqué sur chaque élément du tableau. Il prend en paramètre l'élément courant, l'index courant et le tableau sur lequel on boucle.

> Pour filtrer il faut `return` une condition. Si cette condition est respectée par l'élément courant, il sera placé dans le nouveau tableau

```js
const monTableau = ['banane', 'poire', 'pomme', 'ananas'];
const tableauFiltre = monTableau.filter((elementCourant, indexCourant, tableau) => {
  // la condition que doivent passer les éléments pour être dans le nouveau tableau : avoir plus de 5 lettres
  return elementCourant.length > 5;
});
// tableauFiltre = ['banane', 'ananas']
```

[Lien vers la doc MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

## find

Méthode de tableau qui permet de **trouver** un élément d'un tableau. Cette méthode prend en argument un callback qui sera appliqué sur chaque élément du tableau. Il prend en paramètre l'élément courant, l'index courant et le tableau sur lequel on boucle.

> Pour trouver il faut `return` une condition. Si cette condition est respectée par l'élément courant il sera renvoyé et on arrêtera la boucle. Si rien n'est trouvé `find` renverra `undefined`

```js
const monTableau = ['banane', 'poire', 'pomme', 'ananas'];
const elementTrouve = monTableau.find((elementCourant, indexCourant, tableau) => {
  // la condition, on veut trouver le 1e élémebt qui a plus de 5 lettres
  return elementCourant.length > 5;
});
// elementTrouve = 'banane';
```

## Destructuring / décomposition

## Tableau

On peut décomposer/destructurer un tableau. Plusieurs étapes sont nécessaires

- préciser le type des variables qui vont stocker les données du tableau (const/let/var)
- mettre les crochets à gauche du égal, pour préciser à JS qu'on est dans un destructuration de tableau
- à droite du égal on met le tableau qu'on destructure
- dans les crochets on vient préciser les noms des variables qui vont stocker les données du tableau

> l'ordre est important, la 1e variable va prendre le 1e élément du tableau, la 2e variable, le 2e élément et ainsi de suite.

```js
const animaux = [
  {
    name: 'canard',
    type: 'oiseau',
  },
  {
    name: 'chat',
    type: 'félin',
  },
  {
    name: 'lion',
    type: 'félin',
  },
  {
    name: 'mouton',
    type: 'ovin',
  }
];
// index  0      1     2     3   
const [canard, chat, lion, mouton] = animaux;
```

> Les noms des variables n'ont pas d'importance

```js
// on peut nommer les const comme on veut,
// ci-dessous ça marche aussi
const [titi, toto, tutu, tata] = animaux;
```

> si on ne veut pas récupérer une des valeur du tableau, on ne met rien

```js
const [canard, chat, , mouton] = animaux;
```

[Lien vers la doc MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring)

## Objet

Pour décomposer/destructurer un objet on doit

- préciser le type des variables qui vont stocker les données de l'objet (const/let/var)
- mettre des accolades à gauche du égal, pour préciser à JS qu'on est dans un destructuration d'un objet
- à droite du égal on met l'objet qu'on va venir destructurer
- dans les accolades on vient préciser les noms des variables qui vont stocker les données des propriétés de l'objet

> Il faut bien mettre les mêmes noms de const que celles des propriétés de l'objet, sinon on aura une valeur à `undefined` pour notre variable

```js
const user = {
  country: 'France',
  firstName: 'Pierre',
  lastName: 'Aldado',
  email: 'p.aldado@oclock.io',
  phone: '0123456789',
  login: 'paldado',
  age: '32',
  lang: 'fr',
};
const { email, login } = user;
```

> l'ordre n'est pas important

```js
const { login, email } = user;
```

> **Les noms des variables est important**

```js
// ici loginUser ne correspond à aucune des propriétés de l'objet user
// la valeur de la const loginUser sera égale à undefined
const { loginUser, email } = user;
```

> on peut renommer les variables dans lesquelles on stocke les données des propriétés {ancienName: newName}

```js
// ici email est réassigner en userEmail
const { login, email: userEmail } = user;
```

[Lien vers la doc MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Object_destructuring)

## Paramètre de fonction

Quand on reçoit un objet en paramètre d'une fonction, on peut destructurer cet objet directement.

```js
const user = {
  country: 'France',
  firstName: 'Pierre',
  lastName: 'Aldado',
  email: 'p.aldado@oclock.io',
  phone: '0123456789',
  login: 'paldado',
  age: '32',
  lang: 'fr',
};
// quand une fonction prend un objet en paramètre, on peut le destructurer directement au niveau des paramètres
function sayHelloToUser({ firstName, lastName }) {
  // on pourra utiliser directement les paramètres destructurer
  // dans les instructions de la fonction
  console.log(`Hello ${firstName} ${lastName}`);
}
// ici j'exécute la fonction sayHelloToUser
// je lui passe l'objet user en argument
sayHelloToUser(user);
```

## Closure

Une closure est une fonction qui renvoie une fonction

```js
function maClosure() {
  return function() {
    console.log('hello');
  }
}
// ici on stocke la fonction renvoyé par maClosure dans une const
const sayHello = maClosure();
// on pourra exécuter plus tard sayHello
sayHello(); // en console => 'hello'
```

Une fonction mémorise son contexte : toutes les données qui lui seront passées au moment de l'exécution seront mémorisées.

```js
function maClosure(greeting) {
  return function() {
    console.log(greeting)
  }
}
const sayHello = maClosure('hello');
const saySalut = maClosure('salut');
// ici la fonction renvoyée par la closure aura mémorisée le paramètre qu'on aura passé
sayHello(); // en console => 'hello'
saySalut(); // en console => 'salut'
```

La fonction retournée peut elle-même prendre des paramètres (comme toutes fonctions). On aura donc, des données qui seront données à la closure et qui seront mémorisée par la fonction renvoyée. Une fois qu'on viendra exécuter cette fonction, on lui donnera des paramètres

```js
function maClosure(greeting) {
  return function(name) {
    console.log(`${greeting} ${name}`);
  }
}
const sayHello = maClosure('hello');
const saySalut = maClosure('salut');
// ici la fonction renvoyée par la closure aura mémorisée le paramètre qu'on aura passé
sayHello('Bob'); // en console => 'hello Bob'
saySalut('Thierry'); // en console => 'salut Thierry'
```
