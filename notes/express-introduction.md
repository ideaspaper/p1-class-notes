[**Back to Home**](./../README.md)

# Express Introduction

> Express.js, or simply Express, is a back end web application framework for Node.js, released as free and open-source software under the MIT License. It is designed for building web applications and APIs.It has been called the de facto standard server framework for Node.js.

[Sumber](https://en.wikipedia.org/wiki/Express.js)

Jika pada materi sebelumnya request dari user didapat melalui CLI, bagaimana membuat request dari user agar dapat diterima melalui web browser? Jawabannya adalah dengan menggunakan Express.js (biasa disebut dengan Express saja). Express dapat di-install pada sebuah aplikasi Node dengan menggunakan bantuan NPM (Node Package Manager).

## NPM

NPM digunakan untuk meng-install semua dependensi, yaitu library-library yang dibutuhkan agar sebuah aplikasi Node dapat berjalan. Umumnya NPM sudah terinstall pada saat kita melakukan instalasi Node. Untuk memeriksa apakah NPM sudah terdapat pada sistem atau tidak, kita dapat menggunakan command di bawah.

```
npm -v
```

Karena kita hendak menggunakan Express, maka kita perlu menginisialisasi folder project kita agar di-maintain oleh NPM. Hal tersebut dapat dilakukan dengan command di bawah.

```
npm init
```

Selanjutnya NPM akan meminta kita menjawab beberapa pertanyaan meliputi informasi aplikasi kita. Jika kita hendak mengisi semua informasi tersebut dengan nilai default, maka kita dapat menambahkan argumen `-y` pada akhir command di atas.

```
npm init -y
```

Jika proses inisialisasi di atas sudah dilakukan, maka NPM akan membuat file `package.json` dalam folder kita. File tersebut berisi informasi-informasi dari project kita dan digunakan oleh NPM untuk mengelola dependensi kita. Langkah selanjutnya adalah instalasi Express yang dapat dilakukan menggunakan command di bawah.

```
npm install express --save
```

Setelah proses instalasi selesai, maka terdapat tambahan pasangan key-value baru berikut.

```json
"dependencies": {
  "express": "4.17.1"
}
```

Selain penambahan di atas, terdapat folder baru juga pada project kita yaitu `node_modules`. Folder ini akan menyimpan semua dependensi yang digunakan oleh aplikasi kita.

## `.gitignore`

Apabila kita hendak mengirimkan source code aplikasi kita agar dapat digunakan oleh developer lain, maka kita tidak perlu menyertakan folder `node_modules`. Hal tersebut dikarenakan, developer lain hanya perlu melakukan command `npm install` untuk melakukan instalasi semua dependensi yang diperlukan. NPM akan mencari file `package.json` kemudian melakukan instalasi semua package yang ada pada key `"dependencies"`. Maka dari itu, folder `node_modules` tidak perlu disertakan pada repository Git. Kita dapat membuat file `.gitignore` untuk keperluan tersebut.

`.gitignore`

```
node_modules
```

## Hello World - Express

Bagaimana kita dapat membuat sebuah aplikasi menggunakan Express? Pertama-tama kita harus membuat sebuah server terlebih dahulu.

```javascript
const express = require("express");
const app = express();
```

Setelah itu, kita harus memerintahkan server tersebut untuk mendengarkan request dari user.

```javascript
app.listen(3000, () => {
  console.log("Server is running and listening");
});
```

Angka 3000 di atas merupakan nilai port default yang digunakan oleh Express. Penulisan di atas bisa dibuat lebih "dinamis" dengan cara membuat variable untuk menampung nilai port.

```javascript
const port = 3000;

app.listen(port, () => {
  console.log("Server is running and listening on port ${port}");
});
```

Setelah itu kita bisa coba mengunjungi `localhost:3000` pada browser kita.

[Sumber](http://expressjs.com/en/starter/hello-world.html)

## Basic Routing

Hasil yang kita dapatkan pada browser dari mengunjungi `localhost:3000` adalah seperti di bawah.

```
Cannot GET /
```

Hal tersebut dikarenakan kita hanya memerintahkan server untuk mendengarkan permintaan koneksi saja. Kita belum memberikan instruksi bagaimana server harus menangani permintaan dari user. Maka dari itu buat kode program menjadi seperti di bawah.

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello world!"); // Bisa berupa Buffer, String, object, Boolean, atau Array
});

app.listen(3000, () => {
  console.log(`Server is listening on port: ${port}`);
});
```

Pada kode program di atas, kita memerintahkan server untuk menangani permintaan `GET` dari user pada endpoint `'/'` yaitu dengan cara mengirimkan pesan `'Hello world!'`. Adapun jenis-jenis permintaan (method) yang umum digunakan adalah seperti di bawah.

| Method | Kegunaan               |
| ------ | ---------------------- |
| GET    | Mengambil data.        |
| POST   | Membuat data baru.     |
| PUT    | Melakukan update data. |
| DELETE | Menghapus data.        |

Kita dapat menambahkan endpoint lainnya seperti di bawah.

```javascript
app.get("/help", (req, res) => {
  res.send("This is help page");
});
```

## Nodemon

Pada saat kita mengubah kode program kita, perubahan tersebut tidak langsung berlaku karena server sudah berjalan. Kita harus me-restart server terlebih dahulu. Karena proses ini cukup merepotkan, maka kita dapat menggunakan bantuan Nodemon pada saat proses development.

Kita dapat menginstall Nodemon dengan cara berikut.

```
# Secara global
npm install -g nodemon

# Secara local, hanya terdapat pada folder project kita
npm install --save-dev nodemon
```

Setelah melakukan instalasi Nodemon, kita dapat menggantikan command `node` dengan `nodemon` untuk menjalankan aplikasi kita.

```
# Jika nodemon di-install secara global
nodemon index.js

# Jika nodemon di-install secara local
npx nodemon index.js
```

Apabila terjadi perubahan pada isi folder project kita, maka nodemon akan melakukan restart secara otomatis.

## Request Params

Sebuah request dapat memiliki parameter. Yang dimaksud dengan parameter adalah value yang dapat dimasukkan oleh user pada sebuah endpoint. Sebagai contoh adalah seperti di bawah.

```javascript
app.get("/greet/:name", (req, res) => {
  const name = req.params.name;
  res.send(`Hello ${name}`);
});
```

Apabila kita memasukkan request `http://localhost:3000/greet/Acong`, maka browser akan menampilkan `Hello Acong`.

Coba sekarang buat kode program di atas menjadi seperti berikut.

```javascript
app.get("/greet/:name", (req, res) => {
  const name = req.params.name;
  res.send(`Hello ${name}`);
});

app.get("/greet/default", (req, res) => {
  const name = req.params.name;
  res.send(`Hello, this is a default greeting`);
});
```

Pada saat kita memasukkan request `http://localhost:3000/greet/default`, pesan apa yang ditampilkan oleh browser?

[Sumber](https://expressjs.com/en/4x/api.html#req.params)

## Reqest Query

`req.query` adalah sebuah object yang akan berisi informasi query yang dikirimkan oleh user. User dapat mengirimkan query menggunakan `?`. Contohnya adalah sebagai berikut.

```javascript
app.get('/testquery', (req, res) => {
  res.send(req.query);
});
```

Kirimkan request `localhost:3000/testquery?name=Acong+Suherman&age=17` menggunakan browser, kemudian amati hasilnya.

[Sumber](http://expressjs.com/en/api.html#req.query)

[**Back to Home**](./../README.md)
