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

[Sumber: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions#Syntax)

[**Back**](./es6-variables-nested-party-process-argv-arrow-function.md)