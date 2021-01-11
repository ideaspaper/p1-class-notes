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
╭─────────╮
│         │ Request
│  User   ├───────────╮
│         │           │
╰─────────╯           │
  ▲                   ▼
  │ Response       ╭──────────────╮
  │                │              │
  │                │              ├───────────╮
  │                │  Controller  │           │ Request
  │                │              │           │ Information
  │                │              │           │
  │                ╰──┬───────────╯           │
  │                   │        ▲              │
  │              Send │        │ Response     │
  │              Data │        │ Information  │
  │                   │        │              ▼
╭─┴────────────╮      │        │       ╭─────────────╮
│              │      │        │       │             │
│              │      │        │       │             │
│     View     │◄─────╯        ╰───────┤    Model    │
│              │                       │             │
│              │                       │             │
╰──────────────╯                       ╰─────────────╯
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

## Practice

Setelah kita memahami konsep di atas, mari kita mencoba membuat aplikasi CRUD (Create, Read, Update, Delete) sederhana. Aplikasi ini tidak menggunakan database dan hanya ditujukan untuk memberi gambaran penerapan konsep MVC sederhana.


[**Back to Home**](./../README.md)