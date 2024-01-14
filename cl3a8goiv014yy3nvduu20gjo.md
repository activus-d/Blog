---
title: "The spread operator and its applicability in javaScript"
seoDescription: "JavaScript ES6 (ECMAScript 6) introduced the spread operator. The spread operator comprises three dots (...) used on iterable objects to expand values..."
datePublished: Tue May 17 2022 14:11:09 GMT+0000 (Coordinated Universal Time)
cuid: cl3a8goiv014yy3nvduu20gjo
slug: the-spread-operator-and-its-applicability-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1652796171457/RtbEEvjl7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1652796432126/_Hramcjt9.png
tags: javascript, web-development, webdev

---

## Introduction

JavaScript ES6 (ECMAScript 6) introduced the spread operator. The spread operator consists of three dots `...` used on iterables, mostly arrays to expand the values in them.

`while expanding values means passing the values in one object as distinct duplicates of another, iterables are objects, which a for loop can loop or iterate over.`

```plaintext
const numbers = [ 1, 2, 3, 4 ]
const numbersClone = [ ...numbers ]
console.log( numbersClone[0] ) //OUTPUT: 1
```

## Spread versus rest operator

Although the spread operator and the rest operator both comprise three dots `...`, they are different in purpose and use.

While the spread operator expands an iterable object into individual elements, the rest operator does the exact opposite by taking the rest values of an object or array and condensing them into a single array.

Similarly, while you can use the spread operator in any position depending on where the expanded values are needed, you can only use the rest operator as a prefix to the last parameter of a function or to the last variable in a destructured object or array:

```plaintext
//AS A FUNCTION PARAMETER
function rest1( a, b, ...args ) { 
	console.log( args ); 
} 
rest1( 1, 2, 3, 4, 5 ); //OUTPUT: [ 3, 4, 5 ]

//AS A VARIABLE IN A DESTRUCTURED ARRAY
const rest2 = [ 1, 2, 3, 4, 5, 6 ]
const [ firstElement, secondElement, thirdElement, ...restOfTheElements ] = rest2
console.log( restOfTheElements ) //OUTPUT: [ 4, 5, 6 ]
```

## Use of the spread operator

### Use the spread operator in place of the `apply()` method:

If you want to use the elements of an array as arguments to a function, you can use the `apply()` method:

```plaintext
function example( a, b, c ) {
    console.log( a, b, c )
}
const myArgs = [ 1, 2, 3 ]
example.apply( null, myArgs ) //OUTPUT: 1 2 3
```

You can do the above easily with the spread operator to give the same output:

```plaintext
function example(a,b,c) { 
    console.log( a, b, c ) 
} 
const myArgs = [ 1, 2, 3 ] 
example( ...myArgs ) //OUTPUT: 1 2 3
```

### Use the spread operator to concatenate arrays

You can also use the spread method instead of the `concat()` method to merge two or more arrays in instances that don't require a large data set:

```plaintext
//USING THE CONCAT() METHOD
let myArr1 = [ 1, 2, 3 ]
const myArr2 = [ 4, 5, 6 ]
const myArr3 = [ 7, 8, 9 ]
myArr1 = myArr1.concat( myArr2, myArr3 )
console.log( myArr1 ) //OUTPUT: [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

//USING THE SPREAD OPERATOR
let myArr1 = [ 1, 2, 3 ] 
const myArr2 = [ 4, 5, 6 ] 
const myArr3 = [ 7, 8, 9 ]
myArr1 = [ ...myArr1, ...myArr2, ...myArr3 ] 
console.log(myArr1) //OUTPUT:  
[ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

### Use the spread operator to make a copy of an array

The spread operator makes it easier for you to make a copy of an array, just like the `slice()` method:

```plaintext
//USING THE SLICE METHOD()
const myArr1 = [ 'a', 'b', 'c', 'd' ]
const myArr2 = myArr1.slice()
console.log( myArr2 ) //OUTPUT: [ 'a', 'b', 'c', 'd' ]

//USING THE SPREAD OPERATOR
const myArr1 = [ 'a', 'b', 'c', 'd' ] 
const myArr2 = [ ...myArr1 ]
console.log( myArr2 ) //OUTPUT: [ 'a', 'b', 'c', 'd' ]
```

However, both the spread operator and the `slice()` method can only make a shallow copy, making them unsuitable for copying multidimensional arrays. This means both the spread operator and the slice method do not create new arrays for internal array elements. They only copy the references to such internal array elements:

```plaintext
//ONE-DIMENSIONAL ARRAY
const myArr1 = [ 1, 2, 3, 4, 5 ]
const myArr2 = [ ...myArr1 ]
myArr2[0] = 'a'
console.log( myArr1 ) //OUTPUT: [ 1, 2, 3, 4, 5 ]
console.log( myArr2 ) //OUTPUT: [ 'a', 2, 3, 4 ]

const myArr1 = [ 1, 2, 3, 4 ] 
const myArr2 = myArr1.slice() 
myArr2[0] = 'a' 
console.log( myArr1 ) //OUTPUT:  [ 1, 2, 3, 4, 5 ] 
console.log( myArr2 ) //OUTPUT:  [ 'a', 2, 3, 4, 5
```

Notice that in both instances above, only the value of the first index of `myArr2` got changed after the reassignment, and it did not affect the first value in `myArr1`,from which `myArr2` was expanded or duplicated from. Now let's try the same method for multidimensional arrays:

```plaintext
//MULTIDIMENSIONAL ARRAY
const myArr1 = [ [ [1, 2], [3, 4] ], 5 ]  
const myArr2 = [ ...myArr1 ]   
myArr2[0][0][0] = 'a'
myArr2[1] = 'b' 
console.log( myArr1 ) //OUTPUT:  [ [ ['a', 2], [3, 4] ], 5 ] 
console.log( myArr2 ) //OUTPUT: [ [ ['a', 2], [3, 4] ], 'b' ]

const myArr1 = [ [ [1, 2], [3, 4] ], 5 ]  
const myArr2 = myArr1.slice()  
myArr2[0][0][0] = 'a'
myArr2[1] = 'b'  
console.log( myArr1 ) //OUTPUT:  [ [ ['a', 2], [3, 4] ], 5 ] 
console.log( myArr2 ) //OUTPUT: [ [ ['a', 2], [3, 4] ], 'b' ]
```

From the instances above, you can see that while in the outputs from the use of the spread operator and the `slice()` method, the value of `[0][0][0]` changed, only the value of `[1]` in `myArr2` changed after re-assignment. This is because the elements in indexes `[0][0][0]` of both arrays are references of the same object and not a copy of the other. The element at `myArr2[1]` is a copy of the element at `myArr1[1]`. Thus, a change in one would not lead to a change in the other.

### Use the spread operator to copy the properties of an object

Use the spread to copy the properties of an existing object into a new one or to add more properties to an existing object:

```plaintext
const obj1 = { name: 'John', age: 32 }
const copyObj1 = { ...obj1 }
const obj2 = { name: 'Femi', location: 'Nigeria' }
const mergeObj = { ...copyObj1, ...obj2 }

console.log( obj1 ) //OUTPUT: { name: 'John', age: 32 }
console.log( copyObj1 ) //OUTPUT: { name: 'John', age: 32 }
console.log( obj2 ) //OUTPUT: { name: 'Femi', location: 'Nigeria' }
console.log( mergeObj ) //OUTPUT: { name: 'Femi', age: 32, location: 'Nigeria' }
```

Notice that the name property of the `mergeObj` takes the value of the latter object. This is because where there are similar properties in the objects you want to merge, the value of the latter object in the merge order is adopted.

### Use the spread operator to create a new array by making an existing array as a Part:

Finally, the spread operator is used to make the elements of an existing array part of a newly created one:

```plaintext
const arr1 = [ 1, 2, 3 ]
const arr2 = [ 7, 8, 9]
const arr3 = [ ...arr1, 4, 5, 6, ...arr2 ]
console.log( arr3 ) //OUTPUT: [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

## Conclusion

In this write-up, you have seen how extensive the use of the spread operator is and how it is different in purpose and use from the rest operator. However, a discussion about the spread operator is not complete without highlighting its defects.

The spread operator is unsuitable where the arguments or values involved are large data sets. This would simply lead to the browser overflowing its stack.

Also, Internet Explorer and older mobile browsers do not provide support for the spread operator.