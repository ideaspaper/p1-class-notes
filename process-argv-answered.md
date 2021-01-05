[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# `process.argv`

Pada saat kita mengeksekusi command `node index.js`, sebenarnya kita dapat memberikan argumen. Argumen tersebut kemudian dapat digunakan oleh kode program pada saat eksekusi.

[Sumber dokumentasi: https://nodejs.org/docs/latest-v14.x/api/process.html#process_process_argv](https://nodejs.org/docs/latest-v14.x/api/process.html#process_process_argv)

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

Buat sebuah program kalkulator `process.argv`.

```javascript
const argv = process.argv;
const userArgs = argv.slice(2);

function calculator(value1, value2, operator) {
  value1 = Number(value1);
  value2 = Number(value2);
  switch (operator) {
    case '+':
      return value1 + value2;
    case '-':
      return value1 - value2;
    case '*':
      return value1 * value2;
    case '/':
      return value1 / value2;
  }
}

console.log(calculator(userArgs[0], userArgs[2], userArgs[1]));
```

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)
