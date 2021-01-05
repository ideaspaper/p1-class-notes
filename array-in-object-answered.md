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

Apabila terdapat array of object seperti di bawah. Bagaimana kita dapat mengakses elemennya?

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
  }
];

// Mengakses id Acong
console.log(participants[0].userId);

// Mengakses email Sitorus
console.log(participants[2].email);

// Mengakses huruf 'd' pada email Djoko
console.log(participants[1].email[0]);

// Mengakses score ke 4 dari Acong
console.log(participants[0].scores[3]);
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
  let highestAvg = 0;
  let highestAvgParticipant;

  for (let i = 0; i < participants.length; i++) {
    let avg = 0;
    for (let j = 0; j < participants[i].scores.length; j++) {
      avg += participants[i].scores[j];
    }
    avg /= participants[i].scores.length;

    if (avg > highestAvg) {
      highestAvg = avg;
      highestAvgParticipant = participants[i];
    }
  }

  return highestAvgParticipant;
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

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)