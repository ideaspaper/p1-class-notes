[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# Multidimensional Array

Array merupakan salah satu tipe struktur data yang mengelompokkan banyak data. Tujuan dari array adalah membuat kumpulan data menjadi terstruktur dan mudah untuk diakses.

```javascript
// Data suhu suatu ruangan
const tempReadings = [26, 26, 28, 30, 31, 29, 28, 26];
```

Array umumnya berisi tipe data yang seragam, seperti pada contoh di atas adalah `number`. Namun pada JavaScript, sebuah array dimungkinkan untuk menampung data-data yang berbeda tipe.

```javascript
// Data seorang user
// user ID, username, email, marital status
const user = [7839, 'Acong', 'a@cong.com', false];
```

Termasuk array.

```javascript
// Kumpulan data user
// user ID, username, email, marital status
const users = [
  [7839, 'Acong', 'a@cong.com', false],
  [7840, 'Djoko', 'd@joko.com', false],
  [7841, 'Sitorus', 's@itorus.com', true]
];
```

Sebuah array yang berisi array seperti di atas disebut juga sebagai multidimensional array. Bagaimana cara mengakses salah satu elemen pada multidimensional array?

```javascript
const users = [
  [7839, 'Acong', 'a@cong.com', false],
  [7840, 'Djoko', 'd@joko.com', false],
  [7841, 'Sitorus', 's@itorus.com', true]
];

// Mengakses id Acong
console.log(users[0][0]);

// Mengakses email Sitorus
console.log(users[2][2]);

// Mengakses huruf 'd' pada email Djoko
console.log(users[1][2][0]);
```

Sebuah array yang berisi array seperti di atas disebut juga sebagai multidimensional array.

## PRACTICE

```javascript
const users = [
  [7839, 'Acong', 'a@cong.com', false],
  [7840, 'Djoko', 'd@joko.com', false],
  [7841, 'Sitorus', 's@itorus.com', true],
  [7842, 'Leony Vitria Hartanti', 'leony@triokwekkwek.com', true],
  [7843, 'Dhea Ananda', 'dhea@triokwekkwek.com', true],
  [7844, 'Alfandy', 'alfandy@triokwekkwek.com', false]
];

// Return value: array user dengan email terpanjang
function longestEmail(users) {
  // Your code here
}

// Return value: array kumpulan user yang belum menikah
function notMarried(users) {
  // Your code here
}

console.log(longestEmail(users));
// [ 7844, 'Alfandy', 'alfandy@triokwekkwek.com', false ]

console.log(notMarried(users));
// [
//   [ 7839, 'Acong', 'a@cong.com', false ],
//   [ 7840, 'Djoko', 'd@joko.com', false ],
//   [ 7844, 'Alfandy', 'alfandy@triokwekkwek.com', false ]
// ]
```

[Answers](./multidimensional-array-answered.md)

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)