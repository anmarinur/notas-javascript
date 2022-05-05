# Métodos y funciones en JavaScript

<br>

## Índice

[Números](#números) | [This](#this) 
--- | --- 
[.bind](#bind) | [isNaN](#isnan)
 | [Math.random](#mathrandom)

<br>

## Números

- [isNaN](#isnan)
- [Math.random](#mathrandom)

<br>

### isNaN

Se usa para evaluar si un elemento no es un número. Retornando un `true` si no es un número y un `false` en caso de serlo.

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

## This

- [.bind](#bind)

<br>

### .bind

Se usa para apuntar el `this` a un objeto deseado. Por ejemplo en el siguiente ejemplo tengo un objeto `persona` con unas propiedads y un método. El `this` que tiene dicho método apunta al objeto `persona` y por lo tanto no hay problema. Pero en la función `greeting` expresada el `this` no apunta al objeto `persona` ya que está expresada fuera del objeto y su this apunta a `window` o el objeto global de donde se esté ejecutando, por lo tanto al invocarla va a dar `undefined` ya que `window.nombre` y `window.apellido` no existen.

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
const greetingPersona = greeting.bind(persona);
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
