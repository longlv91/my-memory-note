# Javascript core note

Author: Long Le

Email: levanlong.91@gmail.com

## Javascript Undefined vs NULL
### What is null?
There are two features of null you should understand:

- null is an empty or non-existent value.
- null must be assigned.

Here’s an example. We assign the value of null to a:

```
let a = null;
console.log(a);
// null
```

### What is undefined?
Undefined most typically means a variable has been declared, but not defined. For example:

```
let b;
console.log(b);
// undefined
```

You can also explicitly set a variable to equal undefined:

```
let c = undefined;
console.log(c);
// undefined
```
Finally, when looking up non-existent properties in an object, you will receive undefined:

```
var d = {};
console.log(d.fake);
// undefined
```

### Similarities between null and undefined
In JavaScript there are only six falsy values. Both null and undefined are two of the six falsy values. Here’s a full list:

- false
- 0 (zero)
- “” (empty string)
- null
- undefined
- NaN (Not A Number)

Any other value in JavaScript is considered truthy.

Also in JavaScript, there are six primitive values. Both null and undefined are primitive values. Here is a full list:

- Boolean
- Null
- Undefined
- Number
- String
- Symbol
All other values in JavaScript are objects (objects, functions, arrays, etc.).

Interestingly enough, when using typeof to test null, it returns object:

```
let a = null;
let b;
console.log(typeof a);
// object
console.log(typeof b);
// undefined
```
This has occurred since the beginning of JavaScript and is generally regarded as a mistake in the original JavaScript implementation.

### null !== undefined
As you can see so far, null and undefined are different, but share some similarities. Thus, it makes sense that null does not strictly equal undefined.

```
null !== undefined
```
But, and this may surprise you, null loosely equals undefined.

```
null == undefined
```
In JavaScript, a double equals tests for loose equality and preforms type coercion. This means we compare two values after converting them to a common type.

### Summary
- null is an assigned value. It means nothing.
- undefined typically means a variable has been declared but not defined yet.
- null and undefined are falsy values.
- null and undefined are both primitives. However an error shows that typeof null = object.
- null !== undefined but null == undefined.