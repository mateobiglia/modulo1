
# Homework JavaScript Avanzado I

## Scope & Hoisting

Determiná que será impreso en la consola, sin ejecutar el código.

> Investiga cuál es la diferencia entre declarar una variable con `var` y directamente asignarle un valor.

```javascript
x = 1;
var a = 5;
var b = 10;
var c = function(a, b, c) { // 8 - 9 - 10
  var x = 10;
  console.log(x);//10 bien 
  console.log(a);//8 bien
  var f = function(a, b, c) {//8 - 9 - 10
    b = a;//8
    console.log(b);//8 bien
    b = c;//8
    var x = 5;
  }
  f(a,b,c);//8 - 9 - 10
  console.log(b);//9 bien
}
c(8,9,10);
console.log(b);//10 bien
console.log(x);//1 bien
```

```javascript
console.log(bar);// undefined
console.log(baz);// yo puse 2 pero la respuesta es error por que baz no esta definido 
foo();
function foo() { console.log('Hola!'); }
var bar = 1;
baz = 2;
```

```javascript
var instructor = "Tony";
if(true) {
    var instructor = "Franco";
}
console.log(instructor);// franco por que el var al estar dentro de un if reemplaza el valor del contexto global
```

```javascript
var instructor = "Tony";
console.log(instructor);//tony
(function() {
   if(true) {
      var instructor = "Franco";
      console.log(instructor);//francoc
   }
})();
console.log(instructor);//tony
```

```javascript
var instructor = "Tony";
let pm = "Franco";
if (true) {
    var instructor = "The Flash";
    let pm = "Reverse Flash";
    console.log(instructor);//the flash
    console.log(pm);//reverse flash
}
console.log(instructor);//the flash
console.log(pm);//franco
```
### Coerción de Datos

¿Cuál crees que será el resultado de la ejecución de estas operaciones?:

```javascript
6 / "3"// 2
"2" * "3"// 6
4 + 5 + "px"// "9px"
"$" + 4 + 5// "$45"
"4" - 2// 2
"4px" - 2// NaN
7 / 0// error
{}[0]// ¿?
parseInt("09")// ¿?
5 && 2// ¿?
2 && 5// ¿?
5 || 0// 5
0 || 5// 0
[3]+[3]-[10]// 23
3>2>1// false
[] == ![]// ¿?
```

> Si te quedó alguna duda repasá con [este artículo](http://javascript.info/tutorial/object-conversion).


### Hoisting

¿Cuál es el output o salida en consola luego de ejecutar este código? Explicar por qué:

```javascript
function test() {
   console.log(a);//undefined
   console.log(foo());//2

   var a = 1;
   function foo() {
      return 2;
   }
}

test();
```

Y el de este código? :

```javascript
var snack = 'Meow Mix';

function getFood(food) {
    if (food) {
        var snack = 'Friskies';
        return snack;
    }
    return snack;
}

getFood(false); // ¿?
```


### This

¿Cuál es el output o salida en consola luego de ejecutar esté código? Explicar por qué:

```javascript
var fullname = 'Juan Perez';
var obj = {
   fullname: 'Natalia Nerea',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function() {
         return this.fullname;
      }
   }
};

console.log(obj.prop.getFullname());//Aurelio de Rosa por que el this.fullname en la funcion getFullname va a hacer
                                    //referencia al fullname dentro de prop: 

var test = obj.prop.getFullname;

console.log(test());// juan perez por que el hace referencia al contexto global
```

### Event loop

Considerando el siguiente código, ¿Cuál sería el orden en el que se muestra por consola? ¿Por qué?

```javascript
function printing() {
   console.log(1); //1
   setTimeout(function() { console.log(2); }, 1000); //5
   setTimeout(function() { console.log(3); }, 0); //4
   console.log(4); //2
}

printing(); //3                        //es en este orden por que primero se va a invocar la funcion printing,luego va
                                       //a ejecutar el console.log(1) y mostrarse por pantalla primero, luego el sto(2)
                                       //va a quedarse a un costado, luego se ejecuta el st0(3) y se queda a una costado
                                       //luego se va "eliminar" la funcion printig, luego el st0(3) ya que tiene duracion //0 y finalmente el sto(2) que tiene 1000 de duracion.
```
