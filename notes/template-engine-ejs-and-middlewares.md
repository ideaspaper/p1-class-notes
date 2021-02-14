# Template Engine EJS and Middlewares

Struktur awal folder project.

```
.
├── .gitignore
├── app.js
├── node_modules
├── package.json
└── package-lock.json
```

## Template Engine EJS

Pada [Express Introduction](./express-introduction.md) kita telah berkenalan dengan method `res.send()`. Method tersebut digunakan untuk mengirimkan informasi pada user. Adapun informasi yang dikirimkan dapat dalam bentuk string biasa ataupun string HTML seperti contoh di bawah.

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send(`
    <body>
      <h1>Hello World!</h1>
    </body>`);
});

app.listen(PORT, () => {
  console.log(`Server is listening on ${PORT}`);
});
```

Apabila kita hendak mengirimkan halaman HTML secara dinamis kita dapat menggunakan cara di bawah. Sebagai contoh kasus, apabila variable `name` bernilai `truthy`, maka akan ditampilkan `Hello <name>!`. Sedangkan jika variable `name` bernilai `falsy`, maka akan ditampilkan `Hello World!`.

```javascript
const name = 'Acong';
const page = `
<body>
  <h1>Hello ${name ? name : 'World'}!</h1>
</body>`;

app.get('/', (req, res) => {
  res.send(page);
});
```

Seperti yang kita lihat di atas, apabila halaman HTML yang hendak ditampilkan menjadi lebih banyak dan kompleks kita akan mengalami kesulitan. Maka dari itu kita dapat memanfaatkan template engine EJS untuk memudahkan pekerjaan kita. Kita dapat melakukan instalasi EJS dengan command `npm install --save ejs`.

Saat kita menggunakan EJS, kita dapat menyiapkan file template HTML (dalam format `*.ejs`) pada folder `views`. File-file tersebut nantinya dapat kita gunakan sewaktu-waktu melalui method `res.render()`. Sebagai contoh, mari kita buat folder `views` dalam folder project kita, dan kita buat file `hello.ejs` dengan isi seperti di bawah.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Hello <%= name %>!</h1>
  </body>
</html>
```

Setelah itu, edit `app.js` JavaScript kita menjadi seperti di bawah.

```javascript
app.set('view engine', 'ejs'); // Set EJS sebagai view engine

app.get('/', (req, res) => {
  // Render akan menggunakan template hello.ejs yang terdapat pada folder views
  // Kita akan memberikan sebuah object yang akan digunakan oleh hello.ejs
  res.render('hello', { name: 'Acong' });
});

app.listen(PORT, () => {
  console.log(`Server is listening on ${PORT}`);
});
```

### `<%= %>`

Yang ada di antara tag `<%= %>` adalah syntax JavaScript yang akan dieksekusi pada saat pemanggilan method `res.render()`. Tag ini akan memberikan output untuk ditampilkan pada halaman HTML. Pada contoh di atas, kita me-render template `hello.ejs` dengan nilai sebuah object yang berisi key `name`. Dengan tag `<%= %>` kita dapat mengakses value dari key object tersebut yang kemudian akan ditampilkan pada halaman HTML.

### `<% %>`

`<% %>` merupakan tag untuk **control-flow**. Contoh dari penggunaan tag ini adalah seperti di bawah. Berbeda dengan tag `<%= %>`, tag ini tidak memberikan output pada halaman HTML.

```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <% if (name) { %>
      <h1>Hello <%= name %>!</h1>
    <% } else { %>
      <h1>Hello World!</h1>
    <% } %>
  </body>
</html>
```

Selain `<%= %>` dan `<% %>`, EJS memiliki tag-tag lain yang dapat kalian explore [di sini](https://ejs.co/).

## Middleware

### Router

Apabila kita memiliki banyak route, kemudian kita meletakkan semua route tersebut pada `app.js` JavaScript kita, `app.js` tersebut akan menjadi rumit dan membingungkan. Maka dari itu, kita bisa memanfaatkan router middleware untuk memisah-misah route kita ke dalam file-file yang lebih kecil. Common practice-nya, file-file router tersebut akan kita letakkan ke dalam folder `routes`. Kita dapat menggunakan router middleware dengan cara seperti yang tercantum [di sini](https://expressjs.com/en/guide/using-middleware.html#middleware.router).

#### Exercise

Buat file `users.json` berikut pada root folder project kita.

```json
[
  {
    "id": 1,
    "username": "Acong",
    "gender": "male",
    "position": "Accounting"
  },
  {
    "id": 2,
    "username": "Djoko",
    "gender": "male",
    "position": "Purchasing"
  },
  {
    "id": 3,
    "username": "Sitorus",
    "gender": "female",
    "position": "Sales"
  }
]
```

1. Buat template EJS untuk menampilkan data semua user dalam bentuk tabel.
1. Buatlah route `GET /users` menggunakan router middleware. Route tersebut akan me-render template EJS pada poin sebelumnya dengan data semua user yang ada.
1. Data yang diberikan ke template EJS harus dalam bentuk array of User (instance).

### Body Parser

Selain melalui request params dan request query, kita dapat mengirimkan input ke server menggunakan form HTML. Contoh dari form HTML adalah seperti di bawah.

```HTML
<form action="/users/add" method="POST">
  <label for="username">Username</label>
  <input type="text" id="username" name="username"><br>
  <input type="radio" id="male" name="gender" value="male" checked>
  <label for="male">Male</label><br>
  <input type="radio" id="female" name="gender" value="female">
  <label for="female">Female</label><br>
  <select name="position" id="position">
    <option>Accounting</option>
    <option>Purchasing</option>
    <option>Sales</option>
  </select><br>
  <input type="submit" value="Submit">
</form>
```

Pada form tersebut, `action` adalah link yang akan dituju saat tombol `Submit` ditekan. Adapun `method` yang digunakan pada contoh di atas adalah `POST` sehingga pada Express kita dapat menangani request tersebut dengan method `post`.

Isi dari form tersebut akan terdapat pada `req.body`. Namun sebelum kita dapat menggunakan `req.body` kita harus menyertakan body parser middleware. Informasi mengenai cara penggunaan middleware tersebut dapat ditemukan [di sini](http://expressjs.com/en/resources/middleware/body-parser.html#expressconnect-top-level-generic).

#### Exercise

1. Buatlah template EJS yang berisi form HTML untuk keperluan menambahkan user. Action dari form tersebut adalah `/users/add` dan method-nya adalah `POST`. Lihat contoh form HTML di atas.
1. Buat route `GET /users/add` untuk me-render template EJS pada poin sebelumnya.
1. Buat route `POST /users/add` untuk menambahkan data user baru ke file `users.json`.
1. Setelah proses penambahan user berhasil, maka lakukan redirect ke `/users`. Informasi mengenai redirect dapat ditemukan [di sini](http://expressjs.com/en/api.html#res.redirect).
1. Semua operasi yang dilakukan harus melibatkan instance User.

### Static

Pada Express, kita dapat mengijinkan user untuk mengakses file-file yang bersifat static seperti gambar, CSS, JavaScript, dll. Hal tersebut dapat kita lakukan mengikuti deskripsi yang ada [di sini](https://expressjs.com/en/starter/static-files.html).

#### Exercise

Berikut adalah contoh CSS untuk styling table yang diambil [dari sini](https://www.w3schools.com/css/css_table.asp) dengan sedikit penyesuaian.

```css
#users {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#users td, #users th {
  border: 1px solid #ddd;
  padding: 8px;
}

#users tr:nth-child(even){background-color: #f2f2f2;}

#users tr:hover {background-color: #ddd;}

#users th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #4CAF50;
  color: white;
}
```

1. Tambahkan folder `public/css` pada root folder project kita.
1. Buat file `style.css` pada folder di poin sebelumnya, dengan isi seperti contoh di atas.
1. Gunakan `style.css` tersebut pada template EJS yang menampilkan semua user dalam bentuk tabel.
