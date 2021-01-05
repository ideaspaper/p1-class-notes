[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# Pass by Reference

Ketika kita hendak menyalin nilai dari sebuah variable maka kita akan melakukan hal di bawah.

```javascript
let a = 10;
let b = a;
console.log(`nilai a: ${a}, nilai b: ${b}`);
```

Bagaimana dengan Array & Object?

```javascript
let a = [39, 40, 41, 42];
let b = a;
console.log('nilai a:', a, 'nilai b:', b); // nilai a: [ 39, 40, 41, 42 ] nilai b: [ 39, 40, 41, 42 ]

b[0] = 10;
console.log('nilai a:', a, 'nilai b:', b); // nilai a: [ 10, 40, 41, 42 ] nilai b: [ 10, 40, 41, 42 ]
```

Ternyata saat kita mengubah nilai elemen 0 dari array `b`, maka nilai elemen 0 dari array `a` juga ikut berubah. Hal ini dikarenakan pada saat kita melakukan `let b = a`, `b` akan menampung alamat memori (reference) dari `a`. Maka dari itu, saat kita mengubah nilai `b`, nilai `a` juga akan berubah karena merujuk pada alamat memori yang sama. Hal yang sama juga terjadi pada object. Perhatikan contoh di bawah.

```javascript
let a = { val1: 39, val2: 40, val3: 41, val4: 42 };
let b = a;
console.log('nilai a:', a, 'nilai b:', b);
// nilai a: { val1: 39, val2: 40, val3: 41, val4: 42 } nilai b: { val1: 39, val2: 40, val3: 41, val4: 42 }

b.val1 = 10;
console.log('nilai a:', a, 'nilai b:', b);
// nilai a: { val1: 10, val2: 40, val3: 41, val4: 42 } nilai b: { val1: 10, val2: 40, val3: 41, val4: 42 }
```

Jadi bagaimana cara kita untuk menyalin sebuah array atau object?

## Shallow Copy

Kita dapat menggunakan [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax). Disebut sebagai shallow copy karena hanya level terluar saja yang akan disalin.

```javascript
let a = [39, 40, 41, 42];
let b = [...a];
console.log('nilai a:', a, 'nilai b:', b); // nilai a: [ 39, 40, 41, 42 ] nilai b: [ 39, 40, 41, 42 ]
b[0] = 10;
console.log('nilai a:', a, 'nilai b:', b); // nilai a: [ 39, 40, 41, 42 ] nilai b: [ 10, 40, 41, 42 ]

let c = [[0, 1, 2, 3], 40, 41, 42];
let d = [...c];
console.log('nilai c:', c, 'nilai d:', d);
// nilai c: [ [ 0, 1, 2, 3 ], 40, 41, 42 ] nilai d: [ [ 0, 1, 2, 3 ], 40, 41, 42 ]
d[0][0] = 10;
d[1] = 99;
console.log('nilai c:', c, 'nilai d:', d);
// nilai c: [ [ 10, 1, 2, 3 ], 40, 41, 42 ] nilai d: [ [ 10, 1, 2, 3 ], 99, 41, 42 ]
```

Pada contoh di atas, saat kita mengganti nilai `d[0][0]`, maka `c[0][0]` akan ikut terganti. Hal tersebut dikarenakan hanya nilai elemen terluar `c` saja yang di-assign ke `d`. Dalam hal ini `c[0]` adalah sebuah array, sehingga yang di-assign ke `d` adalah sebuah reference.

## Deep Copy

Tidak seperti shallow copy, deep copy akan menyalin semua elemen sampai ke dalam. Kita dapat memanfaatkan [JSON.parse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse) dan [JSON.stringify](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) untuk keperluan deep copy.

```javascript
let a = [39, 40, 41, 42];
let b = JSON.parse(JSON.stringify(a));
console.log('nilai a:', a, 'nilai b:', b);
// nilai a: [ 39, 40, 41, 42 ] nilai b: [ 39, 40, 41, 42 ]
b[0] = 10;
console.log('nilai a:', a, 'nilai b:', b);
// nilai a: [ 39, 40, 41, 42 ] nilai b: [ 10, 40, 41, 42 ]

let c = [[0, 1, 2, 3], 40, 41, 42];
let d = JSON.parse(JSON.stringify(c));
console.log('nilai c:', c, 'nilai d:', d);
// nilai c: [ [ 0, 1, 2, 3 ], 40, 41, 42 ] nilai d: [ [ 0, 1, 2, 3 ], 40, 41, 42 ]
d[0][0] = 10;
d[1] = 99;
console.log('nilai c:', c, 'nilai d:', d);
// nilai c: [ [ 0, 1, 2, 3 ], 40, 41, 42 ] nilai d: [ [ 10, 1, 2, 3 ], 99, 41, 42 ]
```

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)