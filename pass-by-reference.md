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

## Menyalin Sebuah Array atau Object

Ada banyak teknik yang dapat digunakan untuk menyalin (clone) array ataupun object. Namun karena kita baru saja belajar mengenai recursive function, berikut adalah contoh implementasi fungsi untuk menyalin sebuah array.

```javascript
function arrClone(array) {
  if (!Array.isArray(array)) {
    return array;
  }
  const result = [];
  for (let i = 0; i < array.length; i++) {
    result.push(arrClone(array[i]));
  }
  return result;
}

let a = [[1, 2], 3];
let b = arrClone(a);
console.log('nilai a:', a, 'nilai b:', b);
// nilai a: [ [ 1, 2 ], 3 ] nilai b: [ [ 1, 2 ], 3 ]
b[0][0] = 10;
console.log('nilai a:', a, 'nilai b:', b);
// nilai a: [ [ 1, 2 ], 3 ] nilai b: [ [ 10, 2 ], 3 ]
```

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)