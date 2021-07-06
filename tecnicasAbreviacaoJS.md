# Técnicas de abreviação de códigos JavaScript + tips

Guia rápido de técnicas de abreviação de código JavaScript, que inclui as formas longas de cada uma, para melhor entendimento, e também pequenas dicas de código.

- [Técnicas de abreviação de códigos JavaScript + tips](#técnicas-de-abreviação-de-códigos-javascript--tips)
  - [1. Operador ternário](#1-operador-ternário)
  - [2. Abreviação de declaração condicional](#2-abreviação-de-declaração-condicional)
  - [3. Abreviação de declaração de variáveis](#3-abreviação-de-declaração-de-variáveis)
  - [4. Abreviação de condicional `if`](#4-abreviação-de-condicional-if)
  - [5. Abreviação de loop `for`](#5-abreviação-de-loop-for)
  - [6. Abreviação de definição condicional](#6-abreviação-de-definição-condicional)
  - [7. Base decimal exponencial](#7-base-decimal-exponencial)
  - [8. Abreviação de propriedades de objetos](#8-abreviação-de-propriedades-de-objetos)
  - [9. Abreviação de Arrow functions](#9-abreviação-de-arrow-functions)
  - [10. Abreviação de retorno implícito](#10-abreviação-de-retorno-implícito)
  - [11. Parâmetros com valor default](#11-parâmetros-com-valor-default)
  - [12. Template literal](#12-template-literal)
  - [13. Desestruturação de atribuição](#13-desestruturação-de-atribuição)
  - [14. String multilinha](#14-string-multilinha)
  - [15. Abreviação para operador de propagação](#15-abreviação-para-operador-de-propagação)
  - [16. Abreviação para parâmetros obrigatórios](#16-abreviação-para-parâmetros-obrigatórios)
  - [17. Abreviação para Array.find](#17-abreviação-para-arrayfind)
  - [18. Object [key] Abreviação](#18-object-key-abreviação)
  - [19. Abreviação de arredondamento](#19-abreviação-de-arredondamento)
  - [20. Abreviação de exponenciação](#20-abreviação-de-exponenciação)
  - [21. Convertendo string para número](#21-convertendo-string-para-número)
  - [22. Atribuição de propriedade do objeto](#22-atribuição-de-propriedade-do-objeto)
  - [23. Abreviação para IndexOf](#23-abreviação-para-indexof)
  - [24. Identificando entradas de um objeto](#24-identificando-entradas-de-um-objeto)
  - [25. Identificando valores de um objeto](#25-identificando-valores-de-um-objeto)
  - [26. Adição condicional de propriedades para objetos](#26-adição-condicional-de-propriedades-para-objetos)
  - [27. Checando se uma propriedade existe no objeto](#27-checando-se-uma-propriedade-existe-no-objeto)
  - [27. Setando nome de propriedade dinamicamente](#27-setando-nome-de-propriedade-dinamicamente)
  - [28. Desestruturação com chave dinâmica](#28-desestruturação-com-chave-dinâmica)
  - [29. Operador a coalecência nula (Nullish Coalescing)](#29-operador-a-coalecência-nula-nullish-coalescing)
  - [30. Encadeamento opcional](#30-encadeamento-opcional)
  - [31. Conversão booleana usando operador '!!'](#31-conversão-booleana-usando-operador-)
  - [32. Checando valores falsos em um vetor](#32-checando-valores-falsos-em-um-vetor)
  - [33. "Achatando" (flattening) vetores de vetores](#33-achatando-flattening-vetores-de-vetores)

## 1. Operador ternário

Forma longa:

```javascript
const x = 20;
let answer;

if (x > 10) {
  answer = "greater than 10";
} else {
  answer = "less than 10";
}
```

Abreviação:

```javascript
const answer = x > 10 ? "greater than 10" : "less than 10";
```

Você também pode aninhar declarações `if`:

```javascript
const answer =
  x > 10 ? "greater than 10" : x < 5 ? "less than 5" : "between 5 and 10";
```

## 2. Abreviação de declaração condicional

Forma longa:

```javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== "") {
  let variable2 = variable1;
}
```

Abreviação:

```javascript
const variable2 = variable1 || "new";
```

Exemplo:

```javascript
let variable1;
let variable2 = variable1 || "bar";
console.log(variable2 === "bar"); // prints true

variable1 = "foo";
variable2 = variable1 || "bar";
console.log(variable2); // prints foo
```

## 3. Abreviação de declaração de variáveis

Forma longa:

```javascript
let x;
let y;
let z = 3;
```

Abreviação:

```javascript
let x,
  y,
  z = 3;
```

## 4. Abreviação de condicional `if`

Forma longa:

```javascript
if (likeJavaScript === true)
```

Abreviação:

```javascript
if (likeJavaScript)
```

Forma longa:

```javascript
let a;
if (a !== true) {
  // do something...
}
```

Abreviação:

```javascript
let a;
if (!a) {
  // do something...
}
```

## 5. Abreviação de loop `for`

Forma longa:

```javascript
const fruits = ['mango', 'peach', 'banana'];
for (let i = 0; i < fruits.length; i++)
```

Abreviação:

```javascript
for (let fruit of fruits)
```

Isso também funciona se você desejar acessar keys de um objeto literal:

```javascript
const obj = { continent: "Africa", country: "Kenya", city: "Nairobi" };
for (let key in obj) console.log(key); // output: continent, country, city
```

Abreviação para Array.forEach:

```javascript
function logArrayElements(element, index, array) {
  console.log("a[" + index + "] = " + element);
}
[2, 5, 9].forEach(logArrayElements);
// a[0] = 2
// a[1] = 5
// a[2] = 9
```

## 6. Abreviação de definição condicional

Forma longa:

```javascript
let dbHost;
if (process.env.DB_HOST) {
  dbHost = process.env.DB_HOST;
} else {
  dbHost = "localhost";
}
```

Abreviação:

```javascript
const dbHost = process.env.DB_HOST || "localhost";
```

## 7. Base decimal exponencial

Forma longa:

```javascript
for (let i = 0; i < 10000; i++) {}
```

Abreviação:

```javascript
for (let i = 0; i < 1e7; i++) {}

// Funcionamento
1 === 1;
1e1 === 10;
1e2 === 100;
1e3 === 1000;
1e4 === 10000;
1e5 === 100000;
```

## 8. Abreviação de propriedades de objetos

Forma longa:

```javascript
const x = 1920,
  y = 1080;
const obj = { x: x, y: y };
```

Abreviação:

```javascript
const obj = { x, y };
```

## 9. Abreviação de Arrow functions

Forma longa:

```javascript
function sayHello(name) {
  console.log("Hello", name);
}

setTimeout(function () {
  console.log("Loaded");
}, 2000);

list.forEach(function (item) {
  console.log(item);
});
```

Abreviação:

```javascript
sayHello = (name) => console.log("Hello", name);

setTimeout(() => console.log("Loaded"), 2000);

list.forEach((item) => console.log(item));
```

## 10. Abreviação de retorno implícito

Forma longa:

```javascript
function calcCircumference(diameter) {
  return Math.PI * diameter;
}
```

Abreviação:

```javascript
calcCircumference = diameter => (
  Math.PI * diameter;
)
```

## 11. Parâmetros com valor default

Forma longa:

```javascript
function volume(l, w, h) {
  if (w === undefined) w = 3;
  if (h === undefined) h = 4;
  return l * w * h;
}
```

Abreviação:

```javascript
volume = (l, w = 3, h = 4) => l * w * h;

volume(2); //output: 24
```

## 12. Template literal

Forma longa:

```javascript
const welcome = "You have logged in as " + first + " " + last + ".";

const db = "http://" + host + ":" + port + "/" + database;
```

Abreviação:

```javascript
const welcome = `You have logged in as ${first} ${last}`;

const db = `http://${host}:${port}/${database}`;
```

## 13. Desestruturação de atribuição

Forma longa:

```javascript
const observable = require("mobx/observable");
const action = require("mobx/action");
const runInAction = require("mobx/runInAction");

const store = this.props.store;
const form = this.props.form;
const loading = this.props.loading;
const errors = this.props.errors;
const entity = this.props.entity;
```

Abreviação:

```javascript
import { observable, action, runInAction } from "mobx";

const { store, form, loading, errors, entity } = this.props;
```

You can even assign your own variable names:

```javascript
const { store, form, loading, errors, entity: contact } = this.props;
```

## 14. String multilinha

Forma longa:

```javascript
const lorem =
  "Lorem ipsum dolor sit amet, consectetur\n\t" +
  "adipisicing elit, sed do eiusmod tempor incididunt\n\t" +
  "ut labore et dolore magna aliqua. Ut enim ad minim\n\t" +
  "veniam, quis nostrud exercitation ullamco laboris\n\t" +
  "nisi ut aliquip ex ea commodo consequat. Duis aute\n\t" +
  "irure dolor in reprehenderit in voluptate velit esse.\n\t";
```

Abreviação:

```javascript
const lorem = `Lorem ipsum dolor sit amet, consectetur
    adipisicing elit, sed do eiusmod tempor incididunt
    ut labore et dolore magna aliqua. Ut enim ad minim
    veniam, quis nostrud exercitation ullamco laboris
    nisi ut aliquip ex ea commodo consequat. Duis aute
    irure dolor in reprehenderit in voluptate velit esse.`;
```

## 15. Abreviação para operador de propagação

Forma longa

```javascript
// joining arrays
const odd = [1, 3, 5];
const nums = [2, 4, 6].concat(odd);

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = arr.slice();
```

Abreviação:

```javascript
// joining arrays
const odd = [1, 3, 5];
const nums = [2, 4, 6, ...odd];
console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```

Diferente da função `concat ()`, você pode usar o operador de propagação para inserir um vetor em qualquer lugar dentro de outro vetor.

```javascript
const odd = [1, 3, 5];
const nums = [2, ...odd, 4, 6];
```

Você também pode combinar o operador de propagação com a notação de desestruturação (ES6):

```javascript
const { a, b, ...z } = { a: 1, b: 2, c: 3, d: 4 };
console.log(a); // 1
console.log(b); // 2
console.log(z); // { c: 3, d: 4 }
```

## 16. Abreviação para parâmetros obrigatórios

Forma longa:

```javascript
function foo(bar) {
  if (bar === undefined) {
    throw new Error("Missing parameter!");
  }
  return bar;
}
```

Abreviação:

```javascript
mandatory = () => {
  throw new Error("Missing parameter!");
};

foo = (bar = mandatory()) => {
  return bar;
};
```

## 17. Abreviação para Array.find

Forma longa:

```javascript
const pets = [
  { type: "Dog", name: "Max" },
  { type: "Cat", name: "Karl" },
  { type: "Dog", name: "Tommy" },
];

function findDog(name) {
  for (let i = 0; i < pets.length; ++i) {
    if (pets[i].type === "Dog" && pets[i].name === name) {
      return pets[i];
    }
  }
}
```

Abreviação:

```javascript
pet = pets.find((pet) => pet.type === "Dog" && pet.name === "Tommy");
console.log(pet); // { type: 'Dog', name: 'Tommy' }
```

## 18. Object [key] Abreviação

Considere este exemplo simple de função de validação:

```javascript
function validate(values) {
  if (!values.first) return false;
  if (!values.last) return false;
  return true;
}

console.log(validate({ first: "Bruce", last: "Wayne" })); // true
```

Abreviação:

```javascript
// object validation rules
const schema = {
  first: {
    required: true,
  },
  last: {
    required: true,
  },
};

// universal validation function
const validate = (schema, values) => {
  for (field in schema) {
    if (schema[field].required) {
      if (!values[field]) {
        return false;
      }
    }
  }
  return true;
};

console.log(validate(schema, { first: "Bruce" })); // false
console.log(validate(schema, { first: "Bruce", last: "Wayne" })); // true
```

## 19. Abreviação de arredondamento

Forma longa:

```javascript
Math.floor(4.9) === 4; //true
```

Abreviação:

```javascript
~~4.9 === 4; //true
```

## 20. Abreviação de exponenciação

Forma longa:

```javascript
Math.pow(2, 3); // 8
Math.pow(2, 2); // 4
Math.pow(4, 3); // 64
```

Abreviação:

```javascript
2 ** 3; // 8
2 ** 4; // 4
4 ** 3; // 64
```

## 21. Convertendo string para número

Forma longa:

```javascript
const num1 = parseInt("100");
const num2 = parseFloat("100.01");
```

Abreviação:

```javascript
const num1 = +"100"; // converts to int data type
const num2 = +"100.01"; // converts to float data type
```

## 22. Atribuição de propriedade do objeto

Considere o seguinte código:

```javascript
let fname = { firstName: "Black" };
let lname = { lastName: "Panther" };
```

```javascript
let full_names = Object.assign(fname, lname);
```

Você também pode usar a notação de desestruturação de objeto, introduzido no ES8:

```javascript
let full_names = { ...fname, ...lname };
```

## 23. Abreviação para IndexOf

Forma longa:

```javascript
if (arr.indexOf(item) > -1) {
  // Confirm item IS found
}

if (arr.indexOf(item) === -1) {
  // Confirm item IS NOT found
}
```

Abreviação:

```javascript
if (~arr.indexOf(item)) {
  // Confirm item IS found
}

if (!~arr.indexOf(item)) {
  // Confirm item IS NOT found
}
```

O operador bit a bit `bitwise(~)` retornará um valor verdadeiro para qualquer coisa, exceto `-1`. Negar é tão simples quanto fazer `!~`. Como alternativa, também podemos usar a função `includes()`:

```javascript
if (arr.includes(item)) {
  // Returns true if the item exists, false if it doesn't
}
```

## 24. Identificando entradas de um objeto

```javascript
const credits = { producer: "John", director: "Jane", assistant: "Peter" };
const arr = Object.entries(credits);
console.log(arr);

/** Output:
[ [ 'producer', 'John' ],
  [ 'director', 'Jane' ],
  [ 'assistant', 'Peter' ]
]
**/
```

## 25. Identificando valores de um objeto

```javascript
const credits = { producer: "John", director: "Jane", assistant: "Peter" };
const arr = Object.values(credits);
console.log(arr);

/** Output:
[ 'John', 'Jane', 'Peter' ]
**/
```

## 26. Adição condicional de propriedades para objetos

```javascript
const condition = true;

const person = {
  id: 1,
  name: 'John Doe',
  ...(condition && { age: 16 }),
}
```

## 27. Checando se uma propriedade existe no objeto

```javascript
const person = { name: 'John Doe', age: 16 };

console.log('age' in person);     // retorna true
console.log('salary' in person);  // retorna false
```

## 27. Setando nome de propriedade dinamicamente

```javascript
const dynamic = 'flavour';

var item = {
  name: 'Biscuit',
  [dynamic]: 'Chocolate',
}

console.log(item); // { name: 'Biscuit', flavour: 'Chocolate' }
```

## 28. Desestruturação com chave dinâmica

```javascript
const templates = {
  'hello': 'Hello there',
  'bye': 'Good bye',
}

const templateName = 'bye';

const { [templateName]: template } = templates;

console.log(template); // retorna 'Good bye'
```

## 29. Operador a coalecência nula (Nullish Coalescing)

```javascript
const foo = null ?? 'Hello';
console.log(foo); // retorna 'Hello'

const bar = 'Not null' ?? 'Hello'
console.log(bar); // retorna 'Not null'

const cannotBeZero = 0 || 1;
console.log(cannotBeZero); // retorna 1

// Em JS, 0 é considerado falso, mas não "null" ou "undefined"
const canBeZero = 0 ?? 1;
console.log(canBeZero); // retorna 0
```

## 30. Encadeamento opcional

```javascript
const book = { id: 1, title: "Title", author: null };

// Geralmente acessamos dessa forma:
console.log(book.author.age); // throws error
console.log(book.author && book.author.age); // retorna null (sem erros)

// Utilizando encadeamento opcional
console.log(book.author?.age); // returna undefined
```

## 31. Conversão booleana usando operador '!!'

```javascript
const greeting = 'Hello there!';
console.log(!!greeting); // retorna true

const noGreeting = '';
console.log(!!noGreeting); // retorna false
```

## 32. Checando valores falsos em um vetor

```javascript
const array = [ null, false, 'Hello', undefined, 0 ];

// filtrando valores falsos
const filtered = array.filter(Boolean);
console.log(filtered); // retorna ['Hello']

// checando se há pelo menos um valor verdadeiro
const anyTruthy = array.some(Boolean);
console.log(anyTruthy); // retorna true

// checando se todos os valores são verdadeiros
const allTruthy = array.every(Boolean);
console.log(allTruthy); //retorna false
```

## 33. "Achatando" (flattening) vetores de vetores

```javascript
const array = [{ id: 1 }, [{ id: 2 }], [{ id: 3 }]];

const flattedArray = array.flat(); // retorna [ { id: 1 }, { id: 2 }, { id: 3 } ]
```
