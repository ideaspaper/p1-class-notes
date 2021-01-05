[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# Arrow Function

ES6 mengenalkan ekspresi alternatif untuk membuat sebuah function, yaitu arrow function. Bagaimana cara kita membuat sebuah function menggunakan ekspresi arrow function? Perhatikan kode program di bawah.

```javascript
function regAddFunction(value1, value2) {
  let result = value1 + value2;
  return result;
}

const arrowAddFunction = (value1, value2) => {
  let result = value1 + value2;
  return result;
}

console.log(regAddFunction(4, 7));
console.log(arrowAddFunction(4, 7));
```

[Referensi syntax arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#Syntax).

## Contoh

```javascript
/**
 * Buat sebuah array baru dari ['Acong', 'Djoko', 'Sitorus'].
 * Nilai masing-masing elemen dari array tersebut adalah:
 * [
 *   'Hi my name is Acong',
 *   'Hi my name is Djoko',
 *   'Hi my name is Sitorus'
 * ]
 */

const names = ['Acong', 'Djoko', 'Sitorus'];

const regGreetings = names.map(function (name) {
  return `Hi my name is ${name}`;
});

const arrowGreetings = names.map(name => `Hi my name is ${name}`);

console.log(regGreetings);
console.log(arrowGreetings);
```

Pada contoh di atas, terlihat salah satu kelebihan dari penggunaan arrow function, yaitu penulisan syntax menjadi lebih sederhana.

Dokumentasi dari fungsi map dapat [dilihat di sini](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)