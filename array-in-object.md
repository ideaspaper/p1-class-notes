[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# Array in Object

Sebuah key pada object literal juga dapat memiliki value sebuah array. Sebagai contoh, adalah seperti di bawah.

```javascript
const participant = {
  userId: 7839,
  username: 'Acong',
  email: 'a@cong.com',
  maritalStatus: false,
  scores: [8, 8, 7, 6]
};
```

## PRACTICE

```javascript
const participants = [
  {
    userId: 7839,
    username: 'Acong',
    email: 'a@cong.com',
    maritalStatus: false,
    scores: [8, 8, 7, 6]
  },
  {
    userId: 7840,
    username: 'Djoko',
    email: 'd@joko.com',
    maritalStatus: false,
    scores: [8, 8, 8, 8]
  },
  {
    userId: 7841,
    username: 'Sitorus',
    email: 's@itorus.com',
    maritalStatus: true,
    scores: [10, 8, 8, 9]
  },
  {
    userId: 7842,
    username: 'Leony Vitria Hartanti',
    email: 'leony@triokwekkwek.com',
    maritalStatus: true,
    scores: [10, 9, 10, 9]
  },
  {
    userId: 7843,
    username: 'Dhea Ananda',
    email: 'dhea@triokwekkwek.com',
    maritalStatus: true,
    scores: [10, 10, 8, 9]
  },
  {
    userId: 7844,
    username: 'Alfandy',
    email: 'alfandy@triokwekkwek.com',
    maritalStatus: false,
    scores: [6, 7, 7, 7]
  }
];

function highestAverageScore(participants) {
  // Your code here
}

console.log(highestAverageScore(participants));
// {
//   userId: 7842,
//   username: 'Leony Vitria Hartanti',
//   email: 'leony@triokwekkwek.com',
//   maritalStatus: true,
//   scores: [ 10, 9, 10, 9 ]
// }
```

[Answers](./array-in-object-answered.md)

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)