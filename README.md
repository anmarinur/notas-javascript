# Métodos y funciones en JavaScript

<br>

## Índice

[Números](#números) | [Otros](#otros) | [This](#this) | [Set](#set) | [Objetos](#objetos)
--- | --- | --- | --- | ---
[isNaN](#isnan) | [typeof](#typeof) | [.bind](#bind) | [.add](#add) | [.forEach](#foreach)
[Math.random](#mathrandom) | | [.call](#call) | [.clear](#clear) | 
  | | | | [.delete](#delete) | | 
  | | | | [.forEach](#foreach) | |
  | | | | [.has](#has) | |

<br>

## Números

- [isNaN](#isnan)
- [Math.random](#mathrandom)

<br>

### isNaN

Se usa para evaluar si un elemento no es un número. Retorna un `true` si no es un número y un `false` en caso de serlo.

```js
isNaN(10);          // false
isNaN("Hola");      // true
isNaN(NaN);         // true
isNaN(undefined);   // true
isNaN({});          // true
isNaN(true);        // false: los valores boolean son tomados como 1 o 0
isNaN(null);        // false: es un tipo de número
isNaN('37');        // false: "33" es convertido al número 33
isNaN('37.37');     // false: "45.62" es convertido al número 45.62
isNaN("37,5");      // true
isNaN('123ABC');    // true
isNaN('');          // false: un string vacío es convertido a 0
isNaN(' ');         // false: un string con solo espacios es convertido a 0
```

<br>

### Math.random

Función que genera un número aleatorio entre 0 y 1 (el 1 no lo incluye). 

```js
Math.random(); // Número mayor o igual a 0 y menor que 1
```
Si se quiere modificar el rango del número aleatorio se puede implementar el siguiente código:

```js
let max = 2;
let min = 1;
Math.random() * (max - min) + min;  // Número mayor o igual a 1 y menor que 2
```

<br>

## Objetos

- [.forEach](#foreach)

## Otros

- [typeof](#typeof)

<br>

### typeof

Operador que devuelve el tipo de un elemento. Su salida es un string. El valor evaluado puede ir dentro de paréntesis pero es opcional.

```js
var miFuncion = function(){console.log("Hola")};
var texto = "Anderson";
var numero = 13;
var miObjeto = {name: "objeto", cantidad: 13};

console.log(typeof miFuncion); // "function"
console.log(typeof texto); // "string"
console.log(typeof numero); // "number"
console.log(typeof miObjeto);  // "object"
```

<br>

## Set

- [.add](#add)
- [.clear](#clear)
- [.delete](#delete)
- [.forEach](#foreach)
- [.has](#has)

<br>

### .add

Agrega un elemento al final de un `set`, siempre y cuando este ya no esté dentro, ya que no permite elementos repetidos.

```js
let set1 = new Set();   

set1.add(3);    // set1 = { 3 }
set1.add(4);    // set1 = { 3, 4 }
set1.add(0);    // set1 = { 3, 4, 0 }
set1.add(4);    // set1 = { 3, 4, 0 } No agrega el 4 porque ya existe dentro del elemento
set1.add("Hola");   // set1 = { 3, 4, 0, "Hola" } 

console.log(set1);
```

<br>

### .clear

Remueve todos los elementos de un `set`.

```js
let set1 = new Set();   

set1.add(3);    // set1 = { 3 }
set1.add(4);    // set1 = { 3, 4 }
set1.add(0);    // set1 = { 3, 4, 0 }
set1.add("Hola");   // set1 = { 3, 4, 0, "Hola" } 

console.log(set1);

set1.clear();   // Remueve todos los elementos de set1

console.log(set1);
```

<br>

### .delete

Remueve el elemento indicado de un `set`.

```js
let set1 = new Set();   

set1.add(3);    // set1 = { 3 }
set1.add(4);    // set1 = { 3, 4 }
set1.add(0);    // set1 = { 3, 4, 0 }
set1.add("Hola");   // set1 = { 3, 4, 0, "Hola" } 

console.log(set1);

set1.delete("Hola");    // Remueve "Hola" de set1

console.log(set1);
```

<br>

### .forEach

Método que recorre un elemento iterable, como arrays, sets. Se usa igual en ambos casos.

```js
// Se puede hacer definiendo la función de esta forma
set1.forEach(function(element) {
    console.log(element);
});

// Se puede también usar arrow function
set1.forEach(element => console.log(element))

// element en ambos casos es la variable en donde se guarda cada elemento iterando.
```

```js
let set1 = new Set();   

set1.add(3);    // set1 = { 3 }
set1.add(4);    // set1 = { 3, 4 }
set1.add(0);    // set1 = { 3, 4, 0 }
set1.add("Hola");   // set1 = { 3, 4, 0, "Hola" } 

console.log(set1);

set1.forEach(element => console.log(element));    // Imprime cada elemento de set1
```

<br>

### .has

Método que retorna un boolean indicando si un elemento existe o no en un `set`.

```js
let set1 = new Set();   

set1.add(3);    // set1 = { 3 }
set1.add(4);    // set1 = { 3, 4 }
set1.add(0);    // set1 = { 3, 4, 0 }
set1.add("Hola");   // set1 = { 3, 4, 0, "Hola" } 

console.log(set1);  // set1 = { 3, 4, 0, "Hola" } 
console.log(set1.has(4));   // true
console.log(set1.has(2));   // false
```

<br>

## This

- [.bind](#bind)
- [.call](#call)

<br>

### .bind

Se usa para apuntar el `this` a un objeto deseado. Por ejemplo en el siguiente ejemplo tengo un objeto `persona` con unas propiedads y un método. El `this` que tiene dicho método apunta al objeto `persona` y por lo tanto no hay problema. Pero en la función expresada `greeting` el `this` no apunta al objeto `persona` ya que está expresada fuera del objeto y su this apunta a `window` o el objeto global de donde se esté ejecutando, por lo tanto al invocarla va a dar `undefined` ya que `window.nombre` y `window.apellido` no existen.

```js
const persona = {
    nombre: "Anderson",
    apellido: "Marín",
    saludo: function(){
        console.log(`Hola ${this.nombre} ${this.apellido}`); // Hola Anderson Marín
    }
}

const greeting = function(){
    console.log(`Hello ${this.nombre} ${this.apellido}`); // Hello undefined undefined
}
``` 

Para solucionarlo se usa bind de la siguiente forma. Se crea una variable y allí se guarda el nombre de la función a la que se le quiere apuntar el this, luego `.bind` y entre paréntesis el objeto al que se quiere apuntar:

```js
const greetingPersona = greeting.bind(persona); // Hello Anderson Marín
```

<br>

>Nota: Aquí no se está ejecutando la función greeting, sino que se está accediendo a la función (que es un objeto, como todo en JS) y su método `.bind`

<br>

Otra forma de utilizar el `.bind` es directamente al crear la función:

```js
const greeting2 = function(){
  console.log(`Hi ${this.nombre} ${this.apellido}`); // Hi Anderson Marín
}.bind(persona);
```

<br>

Además de "bindear" al this, también se pueden bindear argumentos de una función. Por ejemplo la función `crearComentario` recibe tres argumentos. Un string inicial, un string final y la cadena de texto a comentar. 

```js
function crearComentario(stringInicial, stringFinal, cadena) {
    return stringInicial + " " + cadena + " " + stringFinal;
}

crearComentario("/*", "*/", "Soy un comentario en JavaScript"); // /* Soy un comentario en JavaScript */
```

Con la anterior función puedo crear nuevas funciones y bindeando algunos argumentos puedo fijarlos para que al final estas solo necesiten de un argumento. Para hacer esto, se asigna a una variable el método de la función y dentro de los argumentos se pone `null` y separado de comas los argumentos que queremos queden fijos en el orden en que aparencen en la función principal.

```js
let comentarioHtml = crearComentario.bind(null, "<--", "-->");  // Tuve que quitar el signo ! porque generaba errores
comentarioHtml("Soy un comentario en HTML"); // <-- Soy un comentario en HTML -->

let negritaMarkdown = crearComentario.bind(null, "**", "**");
negritaMarkdown("Negrita en markdown"); // ** Negrita en markdown **
```

<br>

### .call

Call es muy similar a [.bind](#bind). Es decir con los dos puedo apuntar el this al objeto que yo quiera. La diferencia es que bind no ejecuta la función bindeada y por eso se debe crear una variable para luego invocarla y así ejecutar la función. Mientras que `call` si invoca la función de una vez:

```js
const persona = {
    nombre: "Anderson",
    apellido: "Marín",
    saludo: function(){
        console.log(`Hola ${this.nombre} ${this.apellido}`); // Hola Anderson Marín
    }
}

const greeting = function(){
    console.log(`Hello ${this.nombre} ${this.apellido}`); // Hello undefined undefined
}

// Con bind es necesario utilizar una variable y luego invocarla
const greetingPersona = greeting.bind(persona);
greetingPersona();

// Con call la función es invocada
greeting.call(persona); // Hello Anderson Marín
``` 