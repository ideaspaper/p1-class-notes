[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# `process.argv`

Pada saat kita mengeksekusi command `node index.js`, sebenarnya kita dapat memberikan argumen. Argumen tersebut kemudian dapat digunakan oleh kode program pada saat eksekusi.

[Sumber: https://nodejs.org/docs/latest-v14.x/api/process.html#process_process_argv](https://nodejs.org/docs/latest-v14.x/api/process.html#process_process_argv)

```javascript
const argv = process.argv;

console.log(argv);
// Command: node index.js hello world JavaScript
// [
//   '/usr/local/bin/node',
//   '/home/anpan/work_documents/p1-class-notes/index.js',
//   'hello',
//   'world',
//   'JavaScript'
// ]
```

- `argv[0]` merupakan process.execPath, yaitu direktori node pada sistem.
- `argv[1]` merupakan path file index.js yang dieksekusi.
- `argv[2]` dst. merupakan argumen yang kita ketikkan pada command.

## Practice

Buat sebuah program kalkulator yang memanfaatkan `process.argv` untuk menerima input user.

[Answers](./process-argv-answered.md)

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)
