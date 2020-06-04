# Immutability and Mutability in Javascript

I usually think that a variable is mutable only if its value can be changed. This may be true to some extent but I find it confusing. 

A quote from [MDN about Mutable variable](https://developer.mozilla.org/en-US/docs/Glossary/Mutable)

> /Mutable/ is a type of variable that can be changed. In [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) , only [objects](https://developer.mozilla.org/en-US/docs/Glossary/Object) and [arrays](https://developer.mozilla.org/en-US/docs/Glossary/Array) are mutable, not [primitive values](https://developer.mozilla.org/en-US/docs/Glossary/primitive) .

So, a number or string are immutable but array and objects are mutable. But also if I have a variable:

```js
var number = 5;
var string = 'Bola';

console.log(number); // Outputs 5
console.log(string); // Outputs Bola

number = number + 1;
string = string + ' Buari';

console.log(number); // Outputs 6
console.log(string); // Outputs Bola Buari
```

This means the variable `number` was changed from `5` to `6` and the variable `string` was changed from `Bola` to `Bola Buari`.🤔

These variable were changed but that does not make them mutable. This actuary mean that when `number` and `string` was changed, they became a new value.

A good example to illustrate this is copying the variables and changing the copied variable. If the variable is mutable the original variable is changed, if its immutable the original variable is not change, since chasing it creates a new variable of it’s own.

```js
var originalNumber = 20;
var copiedNumber = originalNumber;
copiedNumber = copiedNumber + 10;

console.log(originalNumber); // Outputs 20 (Not changed)

var originalString = 'Bola';
var copiedString = originalString;
copiedString = copiedString + ' Buari';

console.log(originalString); // Outputs Bola (Not changed)

var originalArray = [1, 2];
var copiedArray = originalArray;
copiedArray.push(3, 4, 5);

console.log(originalArray); // Outputs [1,2,3,4,5] (Changed)

var originalObject = { name: 'Bola', gender: 'Male' };
var copiedObject = originalObject;
copiedObject.job = 'Developer';

console.log(originalObject); // Outputs {name: 'Bola', gender: 'Male', job: 'Developer'} (Changed)
```

As seen in the above examples, when copies of array and object are changed, the original variable is changed while for primitive types like string and number, the original variables are not changed.

What makes me understand immutability more clearly is this, immutable variables are variables that do not change when their copy are changed while mutable variables changes when their copy are changed.

### Resources

- [Mutable - MDN Web Docs Glossary: Definitions of Web-related terms | MDN](https://developer.mozilla.org/en-US/docs/Glossary/Mutable)
