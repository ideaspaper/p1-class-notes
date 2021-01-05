[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# `var`, `let`, `const`

## Scope

```javascript
// Global scope
var a = 'Hello';
let b = 'World';
const c = 'JavaScript';

function myFunction() {
  // Function scope
  var d = 10;
  let e = 20;
  const f = 30;
}

{
  // Block scope
  var g = 40;
  let h = 50;
  const i = 60;
}

console.log(a);
console.log(b);
console.log(c);
console.log(d);
console.log(e);
console.log(f);
console.log(g);
console.log(h);
console.log(i);
```

## `var`

### Scope

`var` digunakan untuk deklarasi variable sebelum revisi ES6. `var` dapat memiliki scope function atau global saja. Perhatikan contoh di bawah.

```javascript
var flag = true;

if (flag) {
  var message = 'flag is true';
} else {
  var message = 'flag is false';
}

console.log(message);
```

Hal di atas mendemonstrasikan salah satu keanehan `var`. `message` seharusnya hanya dikenali di dalam `if`, namun masih dapat diakses di luar scope `if`. Hal ini dikarenakan, `var` hanya dapat memiliki scope function atau global. Apabila `var` tidak terletak di dalam function, maka dia dianngap memiliki scope global.

### Redeclaration

`var` dapat dideklarasi ulang. Perhatikan contoh di bawah.

```javascript
var a = 'Hello World';
var a = false;

console.log(a);
```

Apabila kita tidak sadar bahwa sebuah nama variable sudah digunakan sebelumnya, hal ini tentu menyebabkan error yang susah untuk di-debug.

### Hoisting

Hoisting merupakan mekanisme pada JavaScript yang akan memindahkan deklarasi variable ke atas scope sebelum dieksekusi. Perhatikan contoh di bawah.

```javascript
console.log (message);
var message = "Hello World";

// Hasil hoisting
// var message;
// console.log(message); // undefined
// greeter = "say hello";
```

## `let` dan `const`

### Scope

`let` dan `const` memiliki scope block (`{}`). Perhatikan contoh di bawah.

```javascript
let flag = true;

if (flag) {
  let message = 'flag is true';
} else {
  let message = 'flag is false';
}

console.log(message);
```

Kode program di atas akan error karena `message` tidak dikenali pada saat pemanggilan `console.log(message)`. `const` memiliki sifat scope yang sama dengan `let`.

### Redeclaration

`let` dan `const` tidak dapat dideklarasi ulang. Perhatikan contoh di bawah.

```javascript
let myMessage = 'Hello World';
const myNumber = 10;

let myMessage = 'JavaScript'; // SyntaxError: Identifier 'myMessage' has already been declared
const myNumber = 42; // SyntaxError: Identifier 'myNumber' has already been declared
```

### Hoisting

`let` dan `const` juga mengalami hoisting. Perbedaan dengan `var`, `let` dan `const` tidak diinisialisasi dengan `undefined`. Maka dari itu kita akan mendapatkan pesan error jika kita hendak menggunakan `let` dan `const` sebelum proses deklarasi. Perhatikan contoh di bawah.

```javascript
console.log(myMessage); // ReferenceError: Cannot access 'myMessage' before initialization
console.log(myNumber); // ReferenceError: Cannot access 'myNumber' before initialization
let myMessage = 'Hello World';
const myNumber = 42;
```

Pesan error di atas menyatakan bahwa `myMessage` dan `myNumber` belum diinisialisasi.

### `let` vs `const`

Perbedaan `let` dengan `const` adalah pada proses update nilai. Nilai `let` dapat di-update, sedangkan `const` tidak dapat di-update.

```javascript
let myMessage = 'Hello World';
const myNumber = 42;

myMessage = 'JavaScript';
myNumber = 10; // TypeError: Assignment to constant variable.
```

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)