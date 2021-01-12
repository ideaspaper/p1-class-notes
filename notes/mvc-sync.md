[**Back to Home**](./../README.md)

# MVC Sync

MVC (model–view–controller) merupakan arsitektur/desain yang memisahkan suatu aplikasi menjadi 3 komponen utama, yaitu:

- `Model`, yang berhubungan dengan semua logic tentang pengolahan **data**.
- `View`, yang berhubungan dengan semua logic tentang **tampilan/UI (user interface)**.
- `Controller`, yang berfungsi sebagai **jembatan** penghubung antara `Model` dengan `View`.

Apa keuntungan dari arsitektur MVC? Beberapa adalah seperti di bawah.

1. **Faster development process**. Pengerjaan suatu website sering kali melibatkan lebih dari satu programmer. Beberapa programmer bertugas untuk mengerjakan bagian front end (User Interface), sedangkan beberapa programmer lainnya bertugas untuk mengerjakan back end (business logic dan database). Pengerjaan parallel seperti ini akan mempersingkat waktu development sebuah aplikasi.
1. **Ability to provide multiple views**. Karena `View` merupakan komponen yang terpisah dari business logic dan database, maka kita dimungkinkan untuk membuat banyak jenis `View`. Sebagai contoh, saat ini aplikasi yang dibuat hanya memiliki tampilan untuk layar komputer. Apabila kedepannya kita diminta membuat tampilan untuk layar smartphone, kita hanya perlu membuat `View` baru saja.
1. **The modification does not affect each other**. Perubahan proses logic pada `Model` tidak akan mempengaruhi kode program pada `View`. Demikian pula sebaliknya, perubahan pada tampilan `View` tidak akan mempengaruhi `Model`.

```
                    ╭──────────────╮
╭────────╮          |              | Request
│        | Request  │              | Information
│  USER  ├─────────►│  CONTROLLER  ├───────────╮
│        │          │              │           │
╰────────╯          │              │           │
  ▲                 ╰──┬───────────╯           │
  │               Send │        ▲              │
  │               Data │        │              │
  │ Response           │        │              ▼
╭─┴────────────╮       │        │       ╭─────────────╮
│              │       │        │       │             │
│              │       │        │       │             │
│     VIEW     │◄──────╯        ╰───────┤    MODEL    │
│              │               Response │             │
│              │            Information │             │
╰──────────────╯                        ╰─────────────╯
```

Proses dari diagram di atas adalah:

1. `User` mengirimkan request yang akan diterima oleh `Controller`.
1. `Controller` akan memproses request tersebut.
   - Apabila request tersebut membutuhkan interaksi dengan data:
     1. `Controller` akan meneruskan request tersebut ke `Model`.
     1. `Controller` akan menerima response (raw) dari `Model`, kemudian mengirimkannya sebagai data ke `View`.
     1. `View` akan memberikan response ke `User`.
   - Apabila request tersebut tidak membutuhkan interaksi dengan data:
     1. `Controller` akan mengirimkan data langsung ke `View`.
     1. `View` akan memberikan response ke `User`.

# Practice

Setelah kita memahami konsep di atas, mari kita mencoba membuat aplikasi CRUD (Create, Read, Update, Delete). Aplikasi ini tidak menggunakan database dan hanya ditujukan untuk memberi gambaran penerapan konsep MVC sederhana.

## Release 0

Kita akan membuat sebuah aplikasi pengolahan data customer dengan CLI. Struktur folder dari aplikasi ini adalah sebagai berikut.

```
.
├── controllers
│   └── Controller.js
├── index.js
├── models
└── views
    └── View.js
```

Kita akan mulai dari langkah paling sederhana, yaitu membuat command `help`. Ingat bahwa command dari `User` merupakan request untuk `Controller`. Karena request ini tidak membutuhkan interaksi dengan data, maka `Controller` akan meneruskannya ke `View`. Selanjutnya, `User` akan mendapatkan respon dari `View`. Gunakan `process.argv` untuk menerima command `help` dari `User` pada `index.js`. Tampilan `View` yang diharapkan dari command `help` adalah seperti di bawah.

```
[Command]
node index.js help

[Tampilan view]
Available commands:
  - help
  - create <name> <age> <privilege>
  - read
  - update <id> <name> <age> <privilege>
  - remove <id>
```

## Release 1

Setelah membuat implementasi command `help`, pada release ini kita akan membuat implementasi command `read`. Tambahkan file `app-db.json` sejajar dengan `index.js`. Isi dari file tersebut adalah seperti di bawah. File ini akan berfungsi sebagai database sederhana kita.

```json
[
  {
    "id": 1,
    "name": "Acong",
    "age": 18,
    "privilege": "Regular"
  },
  {
    "id": 2,
    "name": "Djoko",
    "age": 19,
    "privilege": "Regular"
  },
  {
    "id": 3,
    "name": "Sitorus",
    "age": 21,
    "privilege": "VIP"
  }
]
```

Saat ini terdapat dua jenis customer yaitu Regular dan VIP. Maka dari itu, mari kita buat class masing-masing dalam file terpisah. Letakkan semua file tersebut ke dalam folder `models`.

`Customer.js`

```javascript
class Customer {
  constructor(id, name, age, privilege) {
    this.id = id;
    this.name = name;
    this.age = age;
    this.privilege = privilege;
  }
}

module.exports = Customer;
```

`CustomerRegular.js`

```javascript
const Customer = require('./Customer');

class CustomerRegular extends Customer {
  constructor(id, name, age) {
    super(id, name, age, 'Regular');
  }
}

module.exports = CustomerRegular;
```

`CustomerVIP.js`

```javascript
const Customer = require('./Customer');

class CustomerVIP extends Customer {
  constructor(id, name, age) {
    super(id, name, age, 'VIP');
  }
}

module.exports = CustomerVIP;
```

Karena terdapat lebih dari satu jenis `Customer`, dan dimungkinkan akan banyak jenis lain kedepannya, maka buatlah juga factory-nya. Letakkan file factory tersebut pada folder `models`. Setelah itu, masih pada folder yang sama, buatlah file `Model.js`. Kerangka kode program dari file tersebut adalah seperti di bawah.

```javascript
class Model {
  static read() {
    // Your code here
    // 1. Baca file app-db.json, kemudian convert hasilnya menjadi array of objects
    // 2. Buat array of instances dari array of objects tersebut
    // 3. Return hasilnya
  }
}

module.exports = Model;
```

Lakukan penyesuaian pada `Controller.js` dan `View.js` sesuai dengan konsep MVC yang telah dipahami. Hasil yang diharapkan dari `View` adalah seperti di bawah.

```
[Command]
node index.js read

[Tampilan view]
READ OPERATION
[
  CustomerRegular {
    id: 1,
    name: 'Acong',
    age: 18,
    privilege: 'Regular'
  },
  CustomerRegular {
    id: 2,
    name: 'Djoko',
    age: 19,
    privilege: 'Regular'
  },
  CustomerVIP { id: 3, name: 'Sitorus', age: 21, privilege: 'VIP' }
]
```

## Release 2

Pada release ini, mari kita coba mengimplementasikan command `create`. Command ini akan membuat sebuah instance baru, kemudian menuliskannya ke `app-db.json`. Buatlah static method baru pada class `Model`. Kerangka kode program dari method tersebut adalah seperti di bawah.

```javascript
static create() {
  // Your code here
  // 1. Baca file app-db.json, kemudian buat array of instances dari hasil pembacaan tersebut
  // 2. Buat sebuah instance customer dengan nomor id yang otomatis increment
  // 3. Push instance tersebut ke array of instances dari poin 1
  // 4. Tulis array of instances tersebut ke file app-db.json
}
```

Lakukan penyesuaian pada `Controller.js` dan `View.js` sesuai dengan konsep MVC yang telah dipahami. Hasil yang diharapkan dari `View` adalah seperti di bawah.

```
[Command]
node index.js create Budi 16 VIP

[Tampilan view]
CREATE OPERATION
Successfully created: CustomerVIP { id: 4, name: 'Budi', age: 16, privilege: 'VIP' }
```

## Release 3

Pada release ini, kita akan mengimplementasikan command `update`. Command ini akan mencari instance yang dimaksud berdasarkan `id`-nya, kemudian mengganti datanya. Buatlah static method baru pada class `Model`. Kerangka kode program dari method tersebut adalah seperti di bawah.

```javascript
static update() {
  // Your code here
  // 1. Baca file app-db.json, kemudian buat array of instances dari hasil pembacaan tersebut
  // 2. Cari instance dengan property index yang sama dengan yang dicari, return false jika tidak ditemukan
  // 3. Buat sebuah instance customer dengan nomor id yang ditemukan pada poin 2
  // 4. Replace instance lama dengan instance baru
  // 5. Tulis array of instances tersebut ke file app-db.json
}
```

Lakukan penyesuaian pada `Controller.js` dan `View.js` sesuai dengan konsep MVC yang telah dipahami. Hasil yang diharapkan dari `View` adalah seperti di bawah.

```
[Command 1]
node index.js update 4 'Budi S.' 19 Regular

[Tampilan view 1]
UPDATE OPERATION
Old data: CustomerVIP { id: 4, name: 'Budi', age: 16, privilege: 'VIP' }
New data: CustomerRegular {
  id: 4,
  name: 'Budi S.',
  age: 19,
  privilege: 'Regular'
}

[Command 2]
node index.js update 5 Uvuvwevwe 25 VIP

[Tampilan view 2]
UPDATE OPERATION
No data found
```

## Release 4

Pada release ini, kita akan mengimplementasikan command `remove` (karena keyword `delete` tidak dapat digunakan ketika mode `'use strict'`). Command ini akan mencari instance yang dimaksud berdasarkan `id`-nya, kemudian menghapusnya. Buatlah static method baru pada class `Model`. Kerangka kode program dari method tersebut adalah seperti di bawah.

```javascript
static remove() {
  // Your code here
  // 1. Baca file app-db.json, kemudian buat array of instances dari hasil pembacaan tersebut
  // 2. Cari instance dengan property index yang sama dengan yang dicari, return false jika tidak ditemukan
  // 3. Remove instance tersebut dari array
  // 4. Tulis array of instances tersebut ke file app-db.json
}
```

Lakukan penyesuaian pada `Controller.js` dan `View.js` sesuai dengan konsep MVC yang telah dipahami. Hasil yang diharapkan dari `View` adalah seperti di bawah.

```
[Command 1]
node index.js remove 4

[Tampilan view 1]
REMOVE OPERATION
Removed data: CustomerRegular {
  id: 4,
  name: 'Budi S.',
  age: 19,
  privilege: 'Regular'
}

[Command 2]
node index.js remove 5

[Tampilan view 2]
REMOVE OPERATION
No data found
```

[Answers](./mvc-sync-answered.md)

[**Back to Home**](./../README.md)