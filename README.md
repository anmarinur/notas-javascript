# Métodos en JavaScript

## Indice

- [This](#this)

## This

- [.bind](#bind)

### .bind

Se usa para apuntar el _this_ a un objeto deseado. Por ejemplo en el siguiente ejemplo tengo un objeto **persona** con unas propiedads y un método. El _this_ que tiene dicho método apunta al objeto _persona_ y por lo tanto no hay problema. Pero en la función _greeting_ expresada el this no apunta al objeto _persona_ ya que está expresada fuera del objeto y su _this_ apunta a _window_ o el objeto global de donde se esté ejecutando, por lo tanto al invocarla va a dar _undefined_ ya que _window.nombre_ y _window.apellido_ no existen.

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

Para solucionarlo se usa bind de la siguiente forma. Se crea una variable y allí se guarda el nombre de la función a la que se le quiere apuntar el this, luego _.bind_ y entre paréntesis el objeto al que se quiere apuntar:

```js
const greetingPersona = greeting.bind(persona);
```

>Nota: Aquí no se está ejecutando la función greeting, sino que se está accediendo a la función (que es un objeto, como todo en JS) y su método .bind

Otra forma de utilizar el _.bind_ es directamente al crear la función:

```js
const greeting2 = function(){
  console.log(`Hi ${this.nombre} ${this.apellido}`); // Hi Anderson Marín
}.bind(persona);
```
