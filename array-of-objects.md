[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# Array of Objects

Cara lain untuk merepresentasikan user di atas adalah menggunakan tipe struktur data object literal.

```javascript
const user = {
  userId: 7839,
  username: 'Acong',
  email: 'a@cong.com',
  maritalStatus: false
};
```

Seperti yang telah disebutkan sebelumnya, bahwa array dapat berisi beragam tipe data, termasuk object.

```javascript
const users = [
  {
    userId: 7839,
    username: 'Acong',
    email: 'a@cong.com',
    maritalStatus: false
  },
  {
    userId: 7840,
    username: 'Djoko',
    email: 'd@joko.com',
    maritalStatus: false
  },
  {
    userId: 7841,
    username: 'Sitorus',
    email: 's@itorus.com',
    maritalStatus: true
  }
];
```

Contoh di atas disebut juga sebagai array of objects.

## PRACTICE

```javascript
const users = [
  {
    userId: 7839,
    username: 'Acong',
    email: 'a@cong.com',
    maritalStatus: false
  },
  {
    userId: 7840,
    username: 'Djoko',
    email: 'd@joko.com',
    maritalStatus: false
  },
  {
    userId: 7841,
    username: 'Sitorus',
    email: 's@itorus.com',
    maritalStatus: true
  },
  {
    userId: 7842,
    username: 'Leony Vitria Hartanti',
    email: 'leony@triokwekkwek.com',
    maritalStatus: true
  },
  {
    userId: 7843,
    username: 'Dhea Ananda',
    email: 'dhea@triokwekkwek.com',
    maritalStatus: true
  },
  {
    userId: 7844,
    username: 'Alfandy',
    email: 'alfandy@triokwekkwek.com',
    maritalStatus: false
  }
];

// Return value: object user dengan email terpanjang
function longestEmail(users) {
  // Your code here
}

// Return value: array kumpulan object user yang belum menikah
function notMarried(users) {
  // Your code here
}

console.log(longestEmail(users));
// {
//   userId: 7844,
//   username: 'Alfandy',
//   email: 'alfandy@triokwekkwek.com',
//   maritalStatus: false
// }

console.log(notMarried(users));
// [
//   {
//     userId: 7839,
//     username: 'Acong',
//     email: 'a@cong.com',
//     maritalStatus: false
//   },
//   {
//     userId: 7840,
//     username: 'Djoko',
//     email: 'd@joko.com',
//     maritalStatus: false
//   },
//   {
//     userId: 7844,
//     username: 'Alfandy',
//     email: 'alfandy@triokwekkwek.com',
//     maritalStatus: false
//   }
// ]
```

[Answers](./array-of-objects-answered.md)

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)