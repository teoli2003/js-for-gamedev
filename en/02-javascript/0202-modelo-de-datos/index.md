# The JavaScript data model

Knowing a programming language basically means to know its syntax, data model,
execution model, and style.

Throughout this lesson,
[you will code into JavaScript what you learnt in the prior lesson](../0201-poo/).

Not all languages allow for a 1:1 transcription of the concepts we have
included in the model. For instance, JavaScript does not feature any mechanisms
that allow for the creation of new types, but it does feature other mechanisms
that allow for the implementation of a similar functionality.

## Experimenting with JavaScript

You are going to experiment with JavaScript, so you will need a quick way of
inspecting expressions and obtaining feedback on what you are doing. The best
way is to use the **Node console.** For instance:

```
sh
$ node --use_strict
```

The `--use_strict` option enables JavaScript's strict mode, which simplifies
some aspects of the language. Strict mode cuts back on some features, but its
benefits outweigh its drawbacks.

Now you can try to insert some expressions:

```
sh
> 40 + 2
42
> var point = { x: 1, y: 1 };
undefined
> point
{ x: 1, y: 1 }
> point.x
1
```

In order to clear the screen, press `ctrl+l`. To exit Node, press `ctrl+c`
twice in succession. If Node seems to be unresponsive while typing an
expression, press `ctrl+c` once to cancel the expression.

If you do not want to deal with the Node console, you can always write a
program and use `console.log()` in order to show expressions on screen.

```js
// in file test.js
console.log(40 + 2);
var point = { x: 1, y: 1 };
console.log(point);
console.log('Coordinate X:', point.x);
```

Now run the program with Node:

```
sh
$ node test.js
42
{ x: 1, y: 1 }
Coordinate X: 1
```

This lesson assumes you will be using a single Node console session, unless
otherwise specified.

You can keep the same session logged on for most of the examples, but should
you find anything unexpected, you should try restarting the console before
doing anything else. In order to restart the console, you have to **exit and
enter again.**

It would be best for you to keep this text opened up in a window (or printed
out), and the Node console on another.

## Primitive types

**Primitive types** is how we call those that come built in with the language
and which allow for the creation of newer, more complex types. The primitive
types in JavaScript are: **boolean**, **number**, **string**, **objects**, and
**functions.**

```js
// You can find more possible values for each of the types in the comments.
var bool = true; // false
var number = 1234.5; // 42, -Infinity, +Infinity
var text = 'I want to be a pirate!'; // "I want to be a pirate"
var object = {}; // [], null
var code = function () { return 42; };
```

You can tell them from others because they respond differently to the `typeof`
operator. See how the types are text strings:

```js
typeof true;
typeof 1234.5;
typeof 'I want to be a pirate!';
typeof {};
typeof function () { return 42; };
```

In JavaScript, it is possible to declare a variable without assigning any value
to it. In this case, the variable's type would be `'undefined'`.

```js
var x;
typeof x;
x = 5; // as soon as we give it a value, its type will cease to be undefined.
typeof x;
```

### Objects in JavaScript

From among all the types, we shall pay special attention to those which values
allow **compositing** with other values. These are of the `'object'` type.

In JavaScript, objects are collections of tagged values. For instance, if we
want to represent the point `(10, 15)` in the XY plane, we can tag the value on
the Y axis with the string `'x'`, and the value on the Y axis with the `'y'`
string.

```js
var point = { 'x': 10, 'y': 15 };
```

Every tag-value pair is called an **object property.** Less strictly, when we
discuss an object's **properties,** we are usually referring to values, while
what we usually mean by **property name** is the tag.

If property names are written according to the JavaScript
[identifier forming rules](https://developer.mozilla.org/en-US/docs/Glossary/Identifier),
the quotes are unnecessary and can be skipped.

```js
var point = { x: 10, y: 10 }; // much more convenient.
```

This is the most frequent case, the _recommended_ one, and the one we shall use
throughout this material; however, you ought to remember that under the hood,
**the property name is a string.**

In order to access an object's properties, we use the brackets `[` `]` with the
property name in between:

```js
point['x'];
point['y'];
```

Again, if we are following the identifier forming rules, we can use the (much
easier to write) **dot notation** to access the property:

```js
point.x;
point.y;
```

We use the assignment operator to change the value of a property:

```js
point.x = 0;
point.y = 0;
point['x'] = 0;
point['y'] = 0;
```

If you access a **property which does not exist,** you will obtain the value
`undefined`:

```js
var label = point.label; // will be undefined. Check it out with typeof.
```

We can create new properties at any time by assigning something to them.

```js
point.label = 'origin';
point;
```

### Arrays

**Arrays** are collections of **ordered data.**

For instance, the command list in a videogame menu:

```js
var menu = ['Attack', 'Defense', 'Inventory'];
```

In this type of objects, order matters. In order to access the different values
we use the **item's index in the array,** between brackets. Indices _begin
from `0`_, and not from `1`.

```js
menu[0];
menu[1];
menu[2];
```

We can check an array's length by accessing the `length` property.

```js
menu.length;
```

Items can be added to the array's end by calling the
[`push`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
method:

```js
menu.push('Magic');
```

An item can also be removed from the end by using the
[`pop`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
method:

```js
menu.pop();
```

An array can be altered (have items added or removed) in any place by using the
[`splice`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
method:

```js
// Inspect the list after every operation.
menu = ['Attack', 'Defense', 'Inventory'];
menu.splice(2, 0, 'Magic'); // add Magic before Inventory.
menu.splice(2, 2, 'Ench. Inventory'); // replace Magic and Inventory with Ench. Inventory.
menu.splice(0, 0, 'Wait'); // add Wait to list beginning.
```

As is the case with objects, we can change any value at any time by using the
assignment operator.

```js
menu[0] = 'Special'; // replace Wait with Special
```

Again, as is the case with objects, we can access a value that does not exist
and retrieve or assign it at any time.

```js
menu;
menu.length;
var item = menu[10];
typeof item; // will be undefined.
menu[10] = 'Secret';
menu;
menu.length;
```

If we assign to an index beyond the current length, **the array will be
extended** until including that index.

#### Making a distinction between objects and arrays

Both arrays and objects have the `'object'` type, therefore it is necessary to
use the [`Array.isArray()`]( https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
method to tell them apart.

```js
var obj = {}; // the void object is as valid as any other.
var arr = []; // an empty list.
typeof obj; // will be object.
typeof arr; // will be object.
Array.isArray(obj); // will be false.
Array.isArray(arr); // will be true.
```

### `null`

There is another last value for the object type, which is `null`. This value
represents the **absence of an object,** and it normally has the following
uses:

- In functions that query about an object, to indicate that the object has not
been found.

- In compositing relationships, to indicate that the composite object no longer
needs the compositing object.

For instance, in an RPG, we can query about the next living enemy in order to
check whether the battle has to continue:

```js
function getNextAliveEnemy() {
  var nextEnemy;
  if (aliveEnemies.length > 0) {
    nextEnemy = aliveEnemies[0];
  }
  else {
    nextEnemy = null;
  }
  return nextEnemy;
}
```

Or, in another example, consider a hero's character sheet:

```js
var hero = { sword: null, shield: null };
hero.sword = { attack: 20, magic: 5 }; // take a sword.
hero.sword = null; // drop a sword.
```

### Object compositing

Objects and arrays allow any compositing of objects. That is to say, their
values can be other objects and arrays, numbers, strings or functions.

The following example shows a possible RPG character sheet:

```js
var hero = {
  name: 'Link',
  life: 100,
  weapon: { kind: 'sword', power: 20, magicPower: 5 },
  defense: { kind: 'shield', power: 5, magicPower: 0 },
  // Inventory in slots. Two empty slots and another with 5 potions.
  inventory: [
    { item: null, count: 0},
    { item: null, count: 0},
    { item: { kind: 'potion', power: 15 }, count: 5}
  ]
};
```

Some properties:

```js
hero.name; // hero's name
hero.weapon.kind; // type of weapon
hero.inventory[0]; // first inventory slot
hero.inventory[0].item; // what is in the first inventory slot
hero.inventory[2].item.power; // power level of the item in the third inventory slot
```

## Identity of objects

In JavaScript, the equality operator is `===` (triple equal.) This allows us to
compare two objects and decide whether **they are equal.** There is also the
inequality operator `!==`, which compares two objects and decides whether
**they are not equal.**

For the types `'bool'`, `'string'`, `'number'` & `'undefined'`, two values are
equal if they are
[of the **same shape**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators):

```js
// All of these comparisons are true.
"Hola" === "Hola";
"Hola" !== "hola";
true === true;
123 === 123.0;
123 !== "123";
123 === 122 + 1; // the expression is first solved, then compared.
undefined === undefined;
```

For the `object` type, two objects are equal only if they refer to the same
object:

```js
({} !== {}); // regardless of the shape, these are two different objects.
({} !== []);
[] !== []; // same as before.
[1, 2, 3] !== [1, 2, 3]; // regardless of the shape, the objects are different.
null === null; // but with null it works, since there is only one null value.
var obj = {};
var sameObj = obj;
var another = {};
sameObj === obj; // it works because both names refer to the same object.
sameObj !== another; // like before, different despite the same shape.
```

## Objects and message passing

JavaScript objects, as well as being able to use code as any other like value,
allow us to codify the concepts of _object_ and _message passing_ from
object-oriented programming.

### Codifying the state

With what we have seen until now, you should have enough knowledge to codify
the state. The **attribute set** of the object in the object-oriented model
translates into the **property set** of JavaScript objects.

In the _Space Invaders_ example, the state of enemies comprised of:

![Enemy state in the Space Invaders model]( images/space-invaders-enemy-state.png)

Se puede codificar mediante:

```js
var enemy = {
  graphic: 'specie01.png',
  currentDirection: 'right',
  position: { x: 10, y: 10 },
  score: 40
};
```

La primera limitación en JavaScript es que **no se puede restringir el acceso
a las propiedades de un objeto** (es decir, no hay propiedades privadas). Así,
nada nos impide poder modificar la posición directamente.

```js
enemy.position.x = 100; // perfectamente válido.
```

Lo único que se puede hacer es desaconsejar al usuario de ese código que utilice
ciertas propiedades. Una práctica muy común en JavaScript es añadir un guión
bajo `_` a los atributos que consideramos que son **privados**:

```js
var enemy = {
  _graphic: 'specie01.png',
  _currentDirection: 'right',
  _position: { x: 10, y: 10 },
  _score: 40
};
```

Pero, insistimos, esto es una convención y se puede seguir accediendo a los
atributos que tengan este guión bajo:

```js
enemy._position.x = 100; // perfectamente válido también.
```

### Codificando la API

Las acciones que forman la API de un objeto, los **métodos**, pueden
implementarse como **funciones** en propiedades de un objeto.

![API del enemigo en el modelado de Space Invaders]( images/space-invaders-enemy-api.png)

```js
var enemy = {
  _graphic: 'specie01.png',
  _currentDirection: 'right',
  _position: { x: 10, y: 10 },
  _score: 40,

  moveLeft: function () { console.log('Going left!'); },
  moveRight: function () { console.log('Going right!'); },
  advance: function () { console.log('Marching forward!'); },
  shoot: function () { console.log('PICHIUM!'); } // (es un láser)
};
```

**Enviar un mensaje** a un objeto consiste sencillamente acceder a la propiedad
del destinatario, que será una función, y llamarla.

```js
enemy.shoot(); // primero accedemos con punto, luego llamamos con ().
enemy.moveLeft();
enemy.moveLeft();
enemy.advance();
enemy['shoot'](); // es lo mismo, acceder con corchetes y llamar con ().
```

Cualquier función puede actuar como método. Para que actúe como un método
tan sólo es necesario **llamarla desde la propiedad de un objeto**. Y, como
cualquier propiedad de un objeto, podemos cambiarla en cualquier momento:

```js
enemy.shoot(); // PICHIUM!
enemy.shoot = function () { console.log('PAÑUM!'); };
enemy.shoot(); // PAÑUM!
```

Ahora bien, observa el siguiente comportamiento:

```js
enemy; // fíjate en la posición.
enemy.moveLeft();
enemy; // fíjate en la posición otra vez.
```

Obviamente, echando un vistazo a lo que hace `moveLeft`, no podríamos decir
que _cambia el estado_ del objeto destinatario del mensaje. ¿Cómo podríamos
solucionarlo?

Como cualquier función puede actuar como método, hace falta una forma de
**referirse al destinatario del mensaje**, si existe. Cuando se usa como un
método, el destinatario se guarda siempre en la variable **`this`**.

Gracias a ella, podemos implementar los métodos de movimiento:

```js
enemy.moveLeft = function () { this._position.x -= 2; };
enemy.moveRight = function () { this._position.x += 2; };
enemy.advance = function () { this._position.y += 2; };
```

Prueba el mismo experimento de antes y observa cómo efectivamente alteramos el
estado del objeto.

```js
enemy; // fíjate en la posición.
enemy.moveLeft();
enemy; // fíjate en la posición otra vez.
```

### El valor the `this`

El valor de `this` es uno de los aspectos más controvertidos de JavaScript.

En otros lenguajes, métodos y funciones son cosas distintas y un método
_siempre_ tiene asociado un –y sólo un- objeto, así que `this` nunca cambia.

Pero en JavaScript, `this` depende de cómo se llame a la función: si se
llama como si fuera una función, o si se llama como si fuera un método.

Considera la siguiente función:

```js
function inspect() {
  // sólo inspecciona this
  console.log('Tipo:', typeof this);
  console.log('Valor:', this);
}
```

Y prueba lo siguiente:

```js
// Piensa qué puede valer this antes de probar cada ejemplo.
var ship1 = { name: 'T-Fighter', method: inspect };
var ship2 = { name: 'X-Wing', method: inspect };
ship1.method();
ship2.method();
inspect();
```

En el último caso, el valor de `this` es `undefined` porque la función no se
está usando como un método, por lo que no hay destinatario.

En JavaScript podemos hacer que cualquier objeto sea `this` en cualquier
función. Para ello usaremos
[`apply`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Function/apply)
en una función.

```js
var onlyNameShip = { name: 'Death Star' };
inspect.apply(onlyNameShip); // hace que this valga onlyNameShip en inspect.
```

A [`this`](http://dmitrysoshnikov.com/ecmascript/javascript-the-core/#this-value)
se le conoce también como **objeto de contexto**, y en este material usaremos
este término de vez en cuando.

## Consideraciones adicionales

### Nombres y valores

Una **variable es un nombre**. Para el programa, quitando algunas excepciones,
los nombres no tienen significado.

Un **valor no es un nombre**. De hecho, sólo las funciones pueden tener nombre
con el fin de poder implementar recursividad y un par de cosas más.

Así que no es lo mismo el nombre `uno` que el valor `1`, y por supuesto, no
es obligatoria ninguna relación coherente entre el nombre y el valor.

```js
var uno = 2; // para el programa tiene sentido, quizás para el programador no.
```

En general, hablando de booleanos, cadenas y números, decimos que los **nombres
guardan valores**, mientras que si hablamos de objetos y funciones decimos que
los **nombres apuntan** a objetos o funciones o **son referencias** a objetos o
funciones.

### Funciones, referencias a funciones y llamadas a funciones

Hay dos formas de definir una función. Una es usando la **declaración de
función** `function`:

```js
// Introduce una variable factorial que apunta a la función factorial.
function factorial(number) {
  if (number === 0) {
    return 1;
  }
  return number * factorial(number - 1);
} // no hace falta un ';' en este caso.
```

En este caso, el nombre de la función (antes de los paréntesis) es obligatorio.
Dar nombre a una función tiene dos implicaciones:

- Permite implementar **llamadas recursivas** como la del ejemplo.

- **Crea un nombre** `factorial` para referirnos a esa función.

La otra forma es usar una **expression de función**. Esta se parece más a como
crearíamos otros valores, como números o cadenas:

```js
// Introduce una variable recursiveFunction que apunta a OTRA funcion factorial.
var recursiveFunction = function factorial(number) {
  if (number === 0) {
    return 1;
  }
  return number * factorial(number - 1);
}; // ahora sí hace falta ';', como en cualquier asignación.
```

En este último caso, hay dos nombres. Uno es el nombre de la función
`factorial`, que existe para poder referirnos a ella dentro del cuerpo de la
función. El otro es la variable `recursiveFunction` que referencia a la función.

La misma función puede referirse desde múltiples variables o, dicho de otra
manera, tener muchos nombres:

```js
var a = recursiveFunction;
var b = recursiveFunction;
a === b; // es cierto, se refieren a la misma función.
a.name; // el nombre de la función no tiene que ver con el de la variable.
b.name; // lo mismo.
recursiveFunction !== factorial;
```

Tampoco podemos confundir la referencia a la función `factorial` y la
llamada a la misma función, por ejemplo: `factorial(10)`.

Con la primera forma **nos referimos al objeto** que encapsula el código que hay
que ejecutar. No requiere parámetros porque **no se quiere ejecutar el código**
sino solamente referirse a la función.

Con la segunda, **pedimos a la función que se ejecute** y por tanto habrá que
aportar todos los parámetros necesarios.

### En JavaScript todo es un objeto

Si, como definición alternativa, consideramos como objeto aquello que puede
responder a un mensaje, resulta que en JavaScript **todo es un objeto**.

Observa los siguiente ejemplos:

```js
true.toString();
3.1415.toFixed(2);
'I want to be a pirate!'.split(' ');
({}).hasOwnProperty('x');
(function (parameter) { return parameter; }).length;
```

## Tipos y constructores de objetos

Hemos comentado que JavaScript no permite modelar tipos nuevos y que
hace falta "dar un rodeo". Esta es una de las principales diferencias con otros
lenguajes orientados a objetos.

Lo que se debe hacer es saltarse el concepto de _tipo_ para abordar directamente
el de **_constructor_**.

![Constructores de objetos](images/space-invaders-constructor-example.png)

Vamos a crear dos funciones constructoras: una para puntos y otra para disparos.

```js
function newPoint(x, y) {
    var obj = {};
    obj.x = x;
    obj.y = y;

    return obj;
}

function newShot(position, velocity) {
    var obj = {};
    obj._position = position;
    obj._velocity = velocity;
    obj.advance = function () {
        this._position.y += this._velocity;
    };

    return obj;
}
```

La forma de las funciones constructoras es muy similar: crear un objeto vacío,
establecer las propiedades del objeto y devolver el nuevo objeto.

Ahora podríamos crear disparos con algo así:

```js
// Velocidad positiva para que se mueva hacia abajo.
var enemyShot = newShot(newPoint(15, 15), 2);

// Velocidad negativa para que se mueva hacia arriba.
var allyShot = newShot(newPoint(15, 585), -2);

enemyShot !== allyShot;
```

### Reaprovechando funcionalidad

El problema con esta aproximación es que estamos creando funciones distintas
para comportamientos idénticos: una función por objeto.

```js
var s1 = newShot(newPoint(15, 15), 2);
var s2 = newShot(newPoint(15, 15), 2);
var s3 = newShot(newPoint(15, 15), 2);
s1.advance !== s2.advance;
s2.advance !== s3.advance;
s3.advance !== s1.advance;
```

Esto es altamente ineficiente, dado que cada función ocupa un espacio distinto
en memoria.

Realmente no son necesarias tantas funciones, sino una solamente actuando sobre
distintos objetos.

Así que es mejor **crear un objeto que contenga únicamente la API**:

```js
var shotAPI = {
    advance: function () {
        this._position.y += this._velocity;
    }
};
```

Y usarlo en la creación del objeto para compartir los métodos de la API:

```js
function newShot(position, velocity) {
    var obj = {};
    obj._position = position;
    obj._velocity = velocity;
    obj.advance = shotAPI.advance;
    return obj;
}
```

Ahora todas las instancias comparten la misma función, pero cada función actúa
sobre el objeto correspondiente gracias al valor de `this`:

```js
var s1 = newShot(newPoint(15, 15), 2);
var s2 = newShot(newPoint(15, 15), 2);
var s3 = newShot(newPoint(15, 15), 2);
s1.advance === s2.advance; // ahora SÍ son iguales.
s2.advance === s3.advance;
s3.advance === s1.advance;
```

Para hacer todavía más fuerte la asociación entre el constructor y la API,
vamos a realizar una pequeña modificación: crear el objeto con
la API como una **propiedad de la función constructora**, quedando así todo
agrupado en el mismo sitio (la función `newShot`).

```js
function newShot(position, velocity) {
    var obj = {};
    obj._position = position;
    obj._velocity = velocity;
    obj.advance = newShot.api.advance;
    return obj;
}

// Una función es un objeto, así que le podemos añadir una propiedad.
newShot.api = {
    advance: function () {
        this._position.y += this._velocity;
    }
};
```

## La cadena de prototipos

JavaScript posee una característica muy representativa y única del lenguaje:
**la cadena de prototipos**.

Puedes experimentar con ella en [Object Playground]( http://www.objectplayground.com/),
una excelente herramienta que te ayudará a visualizarla.

La idea no es complicada: la cadena de prototipos **es una lista de búsqueda
para las propiedades**. Cada elemento de la cadena es **prototipo** del
objeto anterior.

Cuando accedes a una propiedad de un objeto, esta propiedad se busca en el
objeto y, si no se encuentra, se busca en el prototipo del objeto, y así
sucesivamente hasta alcanzar la propiedad o el final de esta cadena.

Por ejemplo:

```
obj1                    obj2               obj3
{ a: 1, b: 2, c: 3} --> { d: 4, e: 5 } --> { f: 6 }
obj1.c -------↑           ↑                  ↑
obj1.d -------------------|                  |
obj1.f --------------------------------------|
obj1.z ------------------------------------------------X
```

Crear esta jerarquía en JavaScript requiere el uso de [`Object.create()`]( https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/create):

```js
// La cadena se monta de atrás hacia adelante.
var obj3 = { f: 6 };
// Encadenamos obj2 a obj3
var obj2 = Object.create(obj3);
obj2.d = 4;
obj2.e = 5;
// Encadenamos obj1 a obj2
var obj1 = Object.create(obj2);
obj1.a = 1;
obj1.b = 2;
obj1.c = 3;

obj1.c;
obj1.d;
obj1.f;
obj1.z; // undefined
```

El método `Object.create()` crea un nuevo objeto vacío (como `{}`) cuyo
prototipo es el objeto pasado como parámetro.

Se puede usar el método [`hasOwnProperty`]( https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)
para determinar si una propiedad pertenece a un objeto sin atravesar la cadena
de prototipos:

```js
obj1.hasOwnProperty('c'); // true
obj1.hasOwnProperty('d'); // false
obj1.hasOwnProperty('f'); // false
obj1.hasOwnProperty('z'); // false

obj2.hasOwnProperty('c'); // false
obj2.hasOwnProperty('d'); // true
obj2.hasOwnProperty('f'); // false
obj2.hasOwnProperty('z'); // false

obj3.hasOwnProperty('c'); // false
obj3.hasOwnProperty('d'); // false
obj3.hasOwnProperty('f'); // true
obj3.hasOwnProperty('z'); // false
```

Se puede usar el método [`Object.getPrototypeOf()`]( https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)
para obtener el prototipo de un objeto:

```js
Object.getPrototypeOf(obj1) === obj2;
Object.getPrototypeOf(obj2) === obj3;
Object.getPrototypeOf(obj3) === Object.prototype;
Object.getPrototypeOf(Object.prototype) === null;
```

## Constructores y cadenas de prototipos

Los prototipos se prestan a ser el lugar ideal para contener la API, que es el
comportamiento común de todos los objetos de un tipo.

```
var obj = newShot()                               newShot.api
{ _position: { x: 10, y: 10 }, _velocity: 2 } --> { advance: function ... };
obj._position.y ------↑                             ↑
obj.advance ----------------------------------------|
obj.goBack ------------------------------------------------------------------X
```

Para crear este enlace, modificaremos nuestro constructor de la siguiente forma:

```js
function newShot(position, velocity) {
    // Con esto la API es el prototipo del objeto.
    var obj = Object.create(newShot.api);
    obj._position = position;
    obj._velocity = velocity;

    return obj;
}

newShot.api = {
    advance: function () {
        this._position.y += this._velocity;
    }
};
```

Prueba ahora a crear un nuevo disparo:

```js
var shot = newShot({x: 0, y: 0}, 2);
shot; // al inspeccionar shot sólo se muestran las propiedades del objeto.
shot.advance; // pero advance existe en su prototipo.
shot.hasOwnProperty('advance'); // false
Object.getPrototypeOf(shot).hasOwnProperty('advance'); // true
```

Si hacemos esto con todos los constructores, pronto encontraremos un patrón:

1. Crear un objeto para contener la API.

2. Implementar la API como propiedades de este objeto.

3. En el constructor, hacer que este objeto sea el prototipo de un nuevo objeto.

4. Establecer las propiedades del nuevo objeto con el estado.

5. Devolver el nuevo objeto.

Sólo los pasos 2 y 4 involucran diferencias de un constructor a otro, todo lo
demás es exactamente igual. Tanto es así, que JavaScript lo tiene en cuenta
y viene con los mecanismos para automatizar los pasos 1, 3 y 5.

Primero, JavaScript permite que _cualquier función_ pueda usarse como
constructor. Por eso, cada vez que escribimos una función, JavaScript crea una
**propiedad de la función llamada `prototype`**, que es un
objeto con una única propiedad `constructor` que apunta a la función.

```js
function anyFunction() {}
anyFunction.prototype;
anyFunction.prototype.constructor === anyFunction;
```

Esto automatiza el paso 1: ya no es necesario el objeto `api` que preparábamos
nosotros manualmente. La propiedad `prototype` es equivalente a la propiedad
`api`.

Ahora, al llamar a la función con el operador `new` delante, se crea un **nuevo
objeto cuyo prototipo es precisamente la propiedad `prototype`** de la función:

```js
var obj = new anyFunction();
var anotherObj = new anyFunction();

// Los objetos son distintos.
obj !== anotherObj;

// Pero sus prototipos son iguales.
Object.getPrototypeOf(obj) === Object.getPrototypeOf(anotherObj);

// Y además son la propiedad prototype de la función.
Object.getPrototypeOf(obj) === anyFunction.prototype;
```

Con esto se automatiza el paso 3: ya no es necesario llamar a `Object.create()`
para establecer la cadena de prototipos entre objeto y API (lo conseguimos
automáticamente al utilizar el operador `new`).

Finalmente, cuando se llama con `new`, la **función recibe como objeto de
contexto (`this`) el elemento que está siendo creado**, lo que nos
permite establecer sus atributos.

```js
function Hero(name) {
    this.name = name;
    this.sword = null;
    this.shield = null;
}

var hero = new Hero('Link');
hero;
```

Si la función no devuelve nada, el **resultado del operador `new` será el
nuevo objeto**. Esto automatiza el paso 5: no es necesario devolver el
nuevo objeto, esta devolución se hace implícita al utilizar `new`.

Observa como quedaría el constructor de un objeto punto:

```js
function Point(x, y) {
    this.x = x;
    this.y = y;
}
```

Y el del disparo:

```js
function Shot(position, velocity) {
    this._position = position;
    this._velocity = velocity;
}

// El prototipo ya existe, pero le añadimos el método advance()
Shot.prototype.advance = function () {
    this._position.y += this._velocity;
};
```

Ahora crear los objetos será cuestión de usar `new`. Emplearemos además nuestro
nuevo tipo punto (`Point`) para pasar la posición al disparo:

```js
var enemyShot = new Shot(new Point(15, 15), 2);
var allyShot = new Shot(new Point(15, 585), -2);
enemyShot !== allyShot;
```

## Herencia

Ya hemos visto cómo crear objetos con atributos y cómo hacerlo eficazmente,
usando constructores y la cadena de prototipos.

Veremos ahora cómo crear una **relación de herencia**. Recordemos el ejemplo de
los enemigos y la nave protagonista de la lección anterior:

![Relación de herencia entre nave y los enemigos y la nave aliada]( images/space-invaders-hierarchy.png)

Necesitaremos nuestros puntos y disparos:

```js
function Point(x, y) {
    this.x = x;
    this.y = y;
}

function Shot(position, velocity) {
    this._position = position;
    this._velocity = velocity;
}

Shot.prototype.advance = function () {
    this._position.y += this._velocity;
};
```

El constructor y los métodos de los enemigos podrían ser:

```js
function Enemy(graphic, position, score) {
    this._graphic = graphic;
    this._currentDirection = 'right';
    this._position = position;
    this._score = score;
}

Enemy.prototype.moveLeft = function () { this._position.x -= 2; };
Enemy.prototype.moveRight = function () { this._position.x += 2; };
Enemy.prototype.advance = function () { this._position.y += 2; };

Enemy.prototype.shoot = function () {
    var firePosition = new Position(this._position.x, this._position.y + 10);
    var shot = new Shot(firePosition, 2);
    return shot;
};
```

Y aquí la implementación de la nave aliada:

```js
function Ally(position) {
    this._graphic = 'ally.png';
    this._position = position;
}

Ally.prototype.moveLeft = function () { this._position.x -= 2; };
Ally.prototype.moveRight = function () { this._position.x += 2; };

Ally.prototype.shoot = function () {
    var firePosition = new Position(this._position.x, this._position.y - 10);
    var shot = new Shot(firePosition, -2);
    return shot;
};
```

Ahora podemos generalizar y pensar en un constructor que capture las propiedades
comunes de ambos tipos:

```js
function Ship(graphic, position) {
    this._graphic = graphic;
    this._position = position;
}

Ship.prototype.moveLeft = function () { this._position.x -= 2; };
Ship.prototype.moveRight = function () { this._position.x += 2; };
```

En este caso, probablemente sea mejor no incluir el método de disparar
`shoot`, ya que unas naves disparan hacia arriba y otras hacia abajo. Tampoco
incluiremos `advance`, puesto que es exclusivo de los enemigos y no de la nave
aliada.

![Jerarquía de constructores](images/space-invaders-hierarchy-constructor.png)

Recuerda que ahora los constructores de la nave aliada y los enemigos pedirán
primero al constructor de nave que cree una nave y luego la personalizarán.

```js
function Enemy(graphic, position, score) {
    Ship.apply(this, [graphic, position]);
    this._currentDirection = 'right';
    this._score = score;
}

function Ally(position) {
    Ship.apply(this, ['ally.png', position]);
}
```

Con [`apply`](
https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Function/apply)
se puede ejecutar una función indicando cuál será su objeto de contexto y sus
parámetros.

Con la configuración anterior, las nuevas instancias de enemigos y aliados
pasarán primero por el constructor de `Ship`, que establecerá los **atributos
comunes** y luego estas instancias serán modificados cada una por el constructor
pertinente para convertirse en enemigos o en aliados.

En cuanto a la API, lo ideal sería contar con una cadena de prototipos de la siguiente manera:

-  Los atributos del enemigo (o del aliado) están en la propia instancia.

-  La API específica del tipo `Enemy` or `Ally` están en la propiedad
`prototype` del constructor de ese tipo.

- La API común a los tipos `Enemy` y `Ally` está en la propiedad `prototype` del
constructor `Ship`.

```
var enemy = new Enemy()             Enemy.prototype      Ship.prototype
{ _position: ..., _score: ... } --> { advance: ... } --> { moveLeft: ... }
enemy._score -----↑                   ↑                    ↑
enemy.advance ------------------------|                    |
enemy.moveLeft --------------------------------------------|
```

Como ocurría con el ejemplo en la sección anterior, hay que crear la cadena
desde atrás hacia adelante. El enlace entre las instancias y los
constructores nos lo proporciona JavaScript al utilizar `new`, pero el enlace
entre la propiedad `prototype` de `Enemy` y la de `Ship` **hay que que
establecerlo manualmente**.

Prueba lo siguiente:

```js
// Inspecciona el prototype de Enemy.
Enemy.prototype;

// Enlaza ambas propiedades prototype.
Enemy.prototype = Object.create(Ship.prototype);

// Inspecciona la propiedad prototype otra vez y busca diferencias.
Enemy.prototype;

// Corrige la propiedad constructor.
Enemy.prototype.constructor = Enemy;

// Añade el método específico del tipo Enemy.
Enemy.prototype.advance = function () {
    this._position.y += 2;
};

// Otro método específico.
Enemy.prototype.shoot = function () {
    var firePosition = new Point(this._position.x, this._position.y + 10);
    var shot = new Shot(firePosition, 2);
    return shot;
};
```

Y para el tipo `Ally`:

```js
// Lo mismo para el aliado.
Ally.prototype = Object.create(Ship.prototype);
Ally.prototype.constructor = Ally;

Ally.prototype.shoot = function () {
    var firePosition = new Point(this._position.x, this._position.y - 10);
    var shot = new Shot(firePosition, -2);
    return shot;
};
```

Ahora sí, ya podemos crear un enemigo y un aliado usando sus constructores:

```js
var enemy = new Enemy('enemy1.png', new Point(10, 10), 40);
var ally = new Ally(new Point(10, 590));

Object.getPrototypeOf(ally) === Ally.prototype;
Object.getPrototypeOf(enemy) === Enemy.prototype;
Ally.prototype !== Enemy.prototype;
Object.getPrototypeOf(Ally.prototype) === Object.getPrototypeOf(Enemy.prototype);
Object.getPrototypeOf(Ally.prototype) === Ship.prototype;
```

También podemos comprobar dónde está cada propiedad:

```js
enemy.hasOwnProperty('_score');
enemy.hasOwnProperty('advance');
enemy.hasOwnProperty('moveLeft');

Enemy.prototype.hasOwnProperty('_score');
Enemy.prototype.hasOwnProperty('advance');
Enemy.prototype.hasOwnProperty('moveLeft');

Ship.prototype.hasOwnProperty('_score');
Ship.prototype.hasOwnProperty('advance');
Ship.prototype.hasOwnProperty('moveLeft');
```

## Polimorfismo

Las relaciones de herencia que acabamos de establecer nos permiten decir que un
enemigo es una instancia del tipo `Enemy`, pero también lo es del tipo `Ship`.
Una misma instancia tiene **múltiples formas gracias a la herencia**. En
programación orientada a objetos a esto se lo llama **polimorfismo**.

Alternativamente, podemos decir que un enemigo es una instancia de `Enemy`
porque tiene la API de `Enemy`, o que es una instancia de `Ship` porque tiene
la API de `Ship`. Esto es equivalente a decir que las propiedades `prototype`
de `Enemy` y `Ship` están en la cadena de prototipos del objeto.

El operador `instanceof` devuelve verdadero si la propiedad `prototype` de la
función a la derecha del operador está en la cadena de prototipos del objeto a
la izquierda del operador.

```js
enemy instanceof Enemy;  // Enemy.prototype es el primer eslabón.
enemy instanceof Ship;   // Ship.prototype es el segundo.
enemy instanceof Object; // Object.prototype, el tercero.

enemy instanceof Ally;   // Ally.prototype no está en la cadena.
```

En lo referente al estado, resulta conveniente saber qué constructor ha
construido el objeto para conocer de un vistazo los atributos que contendrá el
mismo. Esto es equivalente a determinar cuál es la función cuya propiedad
`prototype` es el **primer eslabón** de la cadena de prototipos.

Dado que los objetos prototipo vienen de serie con una propiedad `constructor`,
que por defecto apunta a la función que posee al objeto prototipo, basta con
acceder a la propiedad `constructor` a través de la instancia.

```js
enemy.constructor;
enemy.constructor === Enemy; // fue construido por Enemy, no por Ship.
enemy.constructor !== Ship; // es cierto que Ship fue utilizado, pero nada más.
```

### Duck typing

> In other words, don't check whether it IS-a duck: check whether it
> QUACKS-like-a duck, WALKS-like-a duck, etc, etc, depending on exactly what
> subset of duck-like behaviour you need to play your language-games with.

[Alex Martelli sobre polimorfismo]( https://groups.google.com/forum/?hl=en#!msg/comp.lang.python/CCs2oJdyuzc/NYjla5HKMOIJ)

La cita se refiere a que más que comprobar si algo es una instancia de un
tipo, se debería comprobar si tiene la funcionalidad que es necesaria.

JavaScript es tan dinámico que el operador `instanceof` y la propiedad
`constructor` sólo tienen sentido si se siguen las convenciones que acabamos de ver.

Nada nos impide borrar la propiedad `constructor` de un prototipo o
sobreescribirla en un objeto determinado. De hecho, en las nuevas versiones de
JavaScript, el prototipo de un objeto puede cambiar después de que el objeto
haya sido construido.