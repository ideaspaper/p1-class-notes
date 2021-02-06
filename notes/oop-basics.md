[**Back to Home**](./../README.md)

# OOP (Object-oriented Programming) Basics

Apa perbedaan pemilik smartphone dengan smartphone-nya? Seorang pemilik smartphone hanya perlu mengetuk layar untuk mendapatkan suatu hasil. Lain halnya dengan smartphone. Sebuah smartphone akan melakukan step-step pekerjaannya dengan detil. Mulai dari menerima sinyal ketukan user, memproses alamat register pada memory, menjalankan rutin program, sampai menampilkan sesuatu di layar.

Apa perbedaan seorang pemilik perusahaan dengan seorang karyawan? Seorang pemilik perusahaan hanya perlu memerintah karyawannya untuk melakukan sesuatu. Pemilik perusahaan hanya mengharapkan hasil. Lain halnya dengan karyawan. Seorang karyawan akan melakukan step-step pekerjaannya dengan detil.

## Object Literal

JavaScript memiliki konsep object literal yang ditujukan untuk **membuat data yang kita miliki menjadi terstruktur**. Kita dapat membuat object literal dengan cara seperti di bawah.

```javascript
const user = {
  name: "Acong",
  birthYear: 1970,
};

console.log(user);
```

Bagaimana jika ada 2 user? Kita dapat menuliskannya seperti di bawah.

```javascript
const user1 = {
  name: "Acong",
  birthYear: 1970,
};

const user2 = {
  name: "Sitorus",
  birthYear: 1975,
};

console.log(user1, user2);
```

Terlihat bahwa kita melakukan suatu hal yang berulang, yaitu menuliskan key. Seperti yang kita tahu, hal tersebut melanggar konsep DRY (don't repeat yourself). Coba amati kode program di bawah. Apa hasil dari kode program tersebut?

```javascript
const users = [];

const user1 = {
  name: "Acong",
  birthYear: 1970,
};

const user2 = {
  nama: "Sitorus",
  birthYear: 1975,
};

users.push(user1, user2);

for (const user of users) {
  console.log(`Hello I am ${user.name}. I am born on ${user.birthYear}.`);
}
```

Kesimpulannya, biarlah object literal berfungsi sebagaimana mestinya, yaitu untuk menstrukturkan data yang kita miliki. Kita tidak menggunakan konsep object literal untuk membuat object dalam konsep OOP yang akan kita pelajari.

## `class`

Keyword `class` digunakan untuk membuat blueprint. Blueprint tersebut nantinya dapat kita gunakan untuk membuat object. Proses membuat object dari sebuah class disebut sebagai **instantiate**.

```javascript
// Blueprint
class User {
  constructor(name, birthYear) {
    this.name = name;
    this.birthYear = birthYear;
  }
}

const user1 = new User('Acong', 1970); // Instantiation, hasilnya adalah object User yang ditampung pada user1
const user2 = new User('Sitorus', 1975); // Instantiation, hasilnya adalah object User yang ditampung pada user2

console.log(user1.name, user1.birthYear); // Mengakses property user1
console.log(user2.name, user2.birthYear); // Mengakses property user2
```

Penggunaan `class` meminimalisir kejadian salah penamaan key pada contoh sebelumnya.

## `constructor`

Kita dapat mendefinisikan properti-properti yang akan dimiliki suatu object di dalam method `constructor`. Seperti namanya, `constructor`, method tersebut hanya akan dipanggil saat kita melakukan instantiation sebuah `class`.

```javascript
user1.constructor(); // TypeError: Class constructor User cannot be invoked without 'new'
```

## Method

Kita dapat membuat function dalam sebuah `class`. Sebuah function yang berada di dalam class akan kita sebut sebagai **method**. Sebuah method memiliki sifat yang sama dengan function, yaitu dapat menerima parameter dan memberikan return value.

```javascript
class User {
  constructor(name, birthYear) {
    this.name = name;
    this.birthYear = birthYear;
  }

  greet() {
    console.log('Hello');
  }
}

const user1 = new User('Acong', 1970);
const user2 = new User('Sitorus', 1975);

user1.greet();
user2.greet();
```

## `this`

Keyword `this` yang ada pada `constructor`, mewakili object itu sendiri. Coba kita tambahkan method `whoAmI` seperti di bawah.

```javascript
class User {
  constructor(name, birthYear) {
    this.name = name;
    this.birthYear = birthYear;
  }

  greet() {
    console.log('Hello');
  }

  whoAmI() {
    console.log(this);
  }
}

const user1 = new User('Acong', 1970);
const user2 = new User('Sitorus', 1975);

user1.whoAmI();
user2.whoAmI();
```

Dapat dilihat bahwa masing-masing object memiliki properti sendiri. Properti `name` pada `user1` memiliki nilai yang berbeda dengan `name` pada `user2`. Coba buat sebuah method `introduce` yang akan menampilkan `Hello my name is [name], I am born on [birthYear]`.

## Method Chaining

Pada saat kita membuat method `whoAmI`, kita menampilkan `this`, yaitu object itu sendiri ke terminal. Bagaimana jika kita mengganti `console.log()` tersebut dengan `return`? Mari kita coba buat method `introduce` seperti di bawah.

```javascript
class User {
  constructor(name, birthYear) {
    this.name = name;
    this.birthYear = birthYear;
  }

  greet() {
    console.log('Hello');
  }

  introduce() {
    console.log(`Hello my name is ${this.name}, I am born on ${this.birthYear}`);
    return this;
  }

  whoAmI() {
    console.log(this);
  }
}

const user1 = new User('Acong', 1970);
const user2 = new User('Sitorus', 1975);

user1.introduce().greet();
user2.introduce().greet();
```

Karena method `introduce` memberikan return `this` yaitu **object** itu sendiri, maka kita bisa memanggil kembali method `greet`. Hal ini disebut juga sebagai method chaining.

## Kenapa OOP?

Seperti line pembuka di atas, dengan OOP kita dapat memerintahkan object-object untuk melakukan sesuatu tanpa harus tahu bagaimana implementasinya. Masih ingat challenge JSRacer? Apabila kita buat versi OOP nya, maka driver code (function `main`) kita menjadi seperti di bawah.

```javascript
const board = new Board(    // Membuat sebuah instance Board
  Number(process.argv[2]),  // Jumlah player
  Number(process.argv[3])   // Panjang track
);

do {
  console.clear();          // Menghapus layar
  board.printBoard();       // Cetak board
  sleep(500);               // Delay selama 500 millisecond
} while (board.nextTurn()); // Next turn, yang akan mereturn true selama belum ada pemenang

board.printWinner();        // Mencetak pemenang
```

Kita hanya perlu membuat instance Board kemudian menjalankan method-method yang tersedia. Kita tidak perlu tahu detil kerja dari setiap method yang ada. Dapat dilihat juga pada driver code di atas kita tidak perlu repot-repot mem-passing arguments seperti waktu kita menerapkan konsep modular function. Hal tersebut dikarenakan setiap instance sudah memiliki data masing-masing (dalam bentuk properti).

Contoh kode program JSRacer versi OOP dapat dilihat [di sini](https://github.com/ideaspaper/p1-jsracer-oop) (private repo hanya untuk keperluan lecture).

[**Back to Home**](./../README.md)
