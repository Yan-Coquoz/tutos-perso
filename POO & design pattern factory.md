Problème: comment créer des objets similaires en boucle dans le code ?

## Design Pattern Factory

C'est un pattern qui permet de construire des objets "en boucle" grace à une fonction.

```javascript
// DP Factory
// On cree une usine a objets pour eviter d'avoir a retaper le code de l'objet a chaque fois

const PizzaFactory = {
    // on cree la methode pour creer les objets. Cette methode contient le moule de nos futurs objets.
    makePizza: (name, base, ingredients) => {

        /* Première notation 
        const newPizza = {};
        newPizza.name = name;
        newPizza.base = base;
        newPizza.ingredients = ingredients; */

        // Seconde notation

        // On definit le moule de nos futurs objets
        const newPizza = {
            name, // equivalent de name:name car même nom
            base, // equivalent de base:base car même nom
            ingredients, // equivalent de ingredients:ingredients...
            print: () => {
                console.log(`La pizza s'appelle ${newPizza.name} et ses ingrédients sont ${newPizza.ingredients.join(' ')}`);
            }
        }

        // nous retourne la pizza créée
        return newPizza;

    }
}

// On cree une premiere pizza
const hawaienne = PizzaFactory.makePizza('Hawaienne', 'Creme fraiche', ['Ananas', 'Jambon']);
// On appelle la methode print de notre objet pizza
hawaienne.print();

// On cree une seconde pizza
const kebab = PizzaFactory.makePizza('kebab', 'Creme fraiche', ['Viande', 'Jambon', 'Tomates', 'Oignons', 'Roquette']);
// On appelle la methode print de notre second objet pizza
kebab.print();
```

## POO

Facon plus élégante de construire des objets et commun à tout les langages.

### this
_this_ est le mot clef qui permet de désigner l'object (l'instance) dans laquel on se trouve actuellement, exemple:

```
// dans une class
constructor() {
    this.value = 42; // refere l'objet que l'on est en train de crée et non la class qui crée cet objet
}
```

### constructor 
C'est une méthode avec un nom fixe qui permet d'initialiser les valeurs de l'objet lorsque celui ci est crée.

Il est optionnel.

```javascript
class Person {
 constructor(name) {
    this.firstname = name;
 }
}

const paul = new Person("Paul");
```

### getter/setter

Les getter et setter javascript sont une syntaxe qui permet de "simplifier" l'écriture des getter/setter traditionnel.

Traditionnel: 
```js
class Person {
    setAge(value) {
        // du code
    }
}

const paul = new Person();

paul.setAge(20); // ok
paul.setAg(20); // error
```

getter/setter:
```js
class Person {
    set age(value) {
        // du code
    }
}

const paul = new Person();

paul.age = 20; // ok
paul.ag = 20; // ok
```

Pour cette raison que les getter/setter permettent ce genre d'erreur, ce n'est pas forcément une bonne pratique. Mais cela reste ouvert au choix du développeur. 

### static

Le mot clef static permet d'associer une variable à la class mere plutot qu'à un objet (instance).

```js
class A {
    foo = 42;
    static bar = 10;
}

const a = new A();

console.log(A.foo); // undefined
console.log(A.bar); // 10

console.log(a.foo); // 42
console.log(a.bar); // undefined
```

### Heritage

On fais hérité une class A d'une class B grace au mot clef extends:
```js
class A extends B {

}
```

La class A récupère alors les propriétés et méthodes de la class B.

#### super

Le mot clef super permet d'accéder à l'instance parent de l'instance que l'on manipule.

```js
class Vehicule {
    hello() {}
}

class Car extends Vehicule {
    constructor() {
        // on appelle le constructor de Vehicule
        super();
    }

    hello() {
        // on appelle la méthode .hello() de Vehicule
        super.hello();
    }
}
```

### instanceof

On utilise le mot clef instanceof pour tester si un objet est une instance d'une class.

```js
class A {}
class B {}

const a = new A();

console.log(a instanceof A); // true
console.log(a instanceof B); // false
```