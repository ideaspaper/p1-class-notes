[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)

# `'use strict'`

`'use strict'` merupakan ekspresi yang menyatakan kode program harus dieksekusi secara strict/ketat. Keuntungan menggunakan `'use strict'` adalah:

- Eliminates some JavaScript silent errors by changing them to throw errors.
- Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
- Prohibits some syntax likely to be defined in future versions of ECMAScript.

[Sumber: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

## Contoh Error

### Kesalahan Deklarasi Variable

```javascript
'use strict';

myMessage = 'Hello World'; // ReferenceError: myMessage is not defined
console.log(myMessage);
```

### Menghapus Variable

```javascript
'use strict';

const myMessage = 'JavaScript';
console.log(myMessage);

delete myMessage; // SyntaxError: Delete of an unqualified identifier in strict mode.
```

### Parameter Function dengan Nama Sama

```javascript
'use strict';

function add (value, value) { // SyntaxError: Duplicate parameter name not allowed in this context
  return value + value;
}

console.log(add(5, 6));
```

### Octal Numeric Literal menyebabkan Error

```javascript
'use strict';

let myNumber1 = 08;
let myNumber2 = 010; // SyntaxError: Octal literals are not allowed in strict mode.
console.log(myNumber1 === myNumber2);
```

### Penggunaan Future Keywords menyebabkan Error

```javascript
'use strict';

let implements = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let interface = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let let = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let package = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let private = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let protected = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let public = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let static = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
let yield = 'Hello World'; // SyntaxError: Unexpected strict mode reserved word
```

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)