---
title: "Destructuring assignment in javaScript"
datePublished: Fri Jun 03 2022 12:54:02 GMT+0000 (Coordinated Universal Time)
cuid: cl3yg6z9a00c4jenv5q27fgzn
slug: destructuring-assignment-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1654260651337/30CMG6IqT.png
tags: programming, javascript, web-development, beginners, frontend-development

---

In this article, I discuss a feature in JavaScript that allows the unpacking of values from iterables and make them into individual variables. This feature is `destructuring assignment`. Destructuring assignment works with any iterable and not just objects or arrays.

```plaintext
An iterable is an object which can be looped over or iterated over with the help of a for loop. 
Objects like lists, sets, and strings are called iterables.
```

## Syntax for destructuring assignment

The syntax is always that the variables taking in the extracted values would be to the left and the iterable that has the values would be to the right. This doesn't change the original iterable. It only copies the items in it into newly declared individual variables:

```javascript
//DESTRUCTURING AN ARRAY 
const x = ["fight", "to", "finish"];  
const [a, b, c] = x;  
console.log(a); // "fight" 
console.log(b); // "to" 
console.log(c); // "finish" 
console.log(x); //  ["fight", "to", "finish"] 

//DESTRUCTURING ITERABLE NOT ARRAY NOR OBJECT 
const [x, y, z] = "bet"; 
console.log(x); // "b" 
console.log(y); // "e" 
console.log(z); // "t"
```

## Assigning values to variables

You can extract values from their variables and assign them to new variables directly with destructuring:

```javascript
const x = [1, 2, 3]; 
const [a, b, c] = x; 
console.log(a); // 1 
console.log(b); // 2 
console.log(c); // 3
```

Also, you can declare variables before assigning them to their values with destructuring. However, in this case, we cannot use `const` to make the declaration:

```javascript
let x, y, z; 
[x, y, z] = [1, 2, 3]; 
console.log(x); // 1  
console.log(y); // 2  
console.log(z); // 3
```

Any remaining variables would be undefined. You can also skip some values using the comma operator:

```javascript
// LESSER VALUES TO UNPACK COMPARED TO NEWLY DECLARED VARIABLES 
const a = [1, 2]; 
const [x, y, z] = a; 
console.log(x); // 1 
console.log(y); // 2 
console.log(z); // undefined

//VALUES 2,3 AND 4 SKIPPED AND NOT UNPACKED 
const a = [1, 2, 3, 4, 5, 6]; 
const [x, , , , y, z] = a; 
console.log(x); // 1  
console.log(y); // 5  
console.log(z); // 6
```

## Using default values

As earlier stated in this article, where the variables declared are more than the values to be unpacked, the extra variables would have the value of undefined. You can avoid this scenario by giving variables in the destructuring expression a default value to be adopted should their values be undefined:

```javascript
const a = [1, 2]; 
const [x = "c", y = "d", z = "f"] = a; 
console.log(x); // 1 
console.log(y); // 2 
console.log(z); // "f"
```

## Destructuring with the Rest Operator

In contrast to declaring more variables than the values to be unpacked, there might also be more values in the iterable than variables declared. Here, you can use the rest operator `...` to take in the remaining values and put them in a single array:

```javascript
const a = [1, 2, 3, 4, 5, 6];
const [x, y, z, ...remainingValues] = a;
console.log(x); // 1 
console.log(y); // 2 
console.log(z); // 3
console.log(remainingValues) // [4, 5, 6]
```

Read about the difference between the rest operator and the spread operator [here](https://activuscode.hashnode.dev/the-spread-operator-and-its-applicability-in-javascript)

## Using destructuring assignment to loop with Object.entries()

The Object.entries() method when used, returns an array with a stringified `[key, value]` property of an object. You can use this method with the `for...of` loop to iterate over the keys and values of an object:

```javascript
let object1 = {
    name: "Femi",
    nationality: "Nigerian",
};
for (let [key, value] of Object.entries(object1)) { 
  console.log(`${key}:${value}`); // name: "Femi", nationality: "Nigerian" 
};
```

You can see from the example above the use of destructuring `[key, value]` in the `for...of` expression.

## Unpacking Properties In Object

Destructuring is also used to assign properties in objects to individual variables. The syntax here is like any other destructuring assignment. To the left side would be the variables that would hold the properties and to the right side would be the object to be destructured from:

```javascript
let object2 = {
    name: "Janet",
    age: 25,
};
let {age, name} = object2;
console.log(name); // "Janet"
console.log(age); // 25
```

Notice that in the above example, even though the order of the newly declared variables didn't follow the order of the properties within object2 they still got assigned to the properties that match their names. However, if the variable name you want to use for the destructuring would differ from the property names of the properties, then you have to use colons to set the variable names like this:

```javascript
let object3 = { 
    name: "Janet", 
    age: 25, 
}; 
let {name: user, age: years} = object3;
console.log(user); // "Janet"
console.log(years); // 25
```

## Destructuring deeply nested iterables

Where an iterable contains objects or arrays as its properties or elements, you can unpack those properties or elements with a similar but more complex left-side syntax. For instance:

```javascript
let object4 = {
    user: {
        name: "John",
        age: 40,
    },
    hobbies: ["swimming", "jumping", "dancing"],
};
//Destructing object4
let {
    user: {
        name,
        age,
    },
    hobbies: [hobby1, hobby2, hobby3],
} = object4
console.log(name); // "John"
console.log(age); // 40
console.log(hobby1); // "swimming"
console.log(hobby2); // "jumping"
console.log(hobby3); // "dancing"
```

## Object Destructuring and Functions

Similarly, you can use destructuring to extract properties of objects passed as a function parameter into variables that can then be accessed within the function body. The variable name to be used in the destructuring syntax can be the same or different from the object's property name. Consider this example:

```javascript
let object5 = { 
    name: "John", 
    age: 30,  
} 
function userInfo({name, age: years}) { 
    return `${name} is ${years} years old` 
} 
userInfo(object5) // "John is 30 years old"
```

It is also possible to assign default values to the parameters within the destructuring syntax. Where you would like to call the function without an argument, you can assign the whole parameters to an empty obj literal like this:

```javascript
let object6 = { 
    name: "John",
    age: 30, 
} 
function userInfo({name = "Jane", age = 50} = {}) { 
    return `${name} is ${age} years old` 
} 
userInfo(object6) // "John is 30 years old"
userInfo() // "Jane is 50 years old"
```

Notice that the function returns the default values when called without an argument. This is because we already assigned it a default object literal. Without that, the function would return an error if called without an argument.

## Conclusion

In this article, you have seen how destructuring assignments can help in creating individual variables from unpacking iterables. Destructuring assignments saves valuable time, which would be spent making individual declarations using, for example, the charAt() method to extract individual items from iterables.
