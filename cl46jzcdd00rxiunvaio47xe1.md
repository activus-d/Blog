---
title: "The Two Simplest Ways to Check if an Object is Empty in JavaScript"
seoDescription: "Use the Object.keys() method and the Object.entries() method to check if an object is empty or not."
datePublished: Thu Jun 09 2022 05:02:14 GMT+0000 (Coordinated Universal Time)
cuid: cl46jzcdd00rxiunvaio47xe1
slug: the-two-simplest-ways-to-check-if-an-object-is-empty-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1654750371014/esGOLkI0E.png
tags: programming, javascript, web-development, webdev, frontend-development

---

Sometimes, while using JavaScript,  it becomes necessary to check if an object is empty or not. This article will provide the two simplest ways to confirm if an object is empty.

## The Use of ```Object.keys()``` Method with the ```Length``` Property
The ```Object.keys()``` method returns an array, which contains the property names of the properties found in the object that ```Object.keys()``` method applies to. For example: 
```javascript
let object1 = {
    name: "Femi",
    age: 30,
    nationality: "Nigerian"
}
console.log( Object.keys(object1) ) // ['name', 'age', 'nationality']
```
You can use ```Object.keys()``` method with the ```length``` property to check for the exact number of properties in an object. If the length property returns 0, then the object is empty. For instance:
```javascript
let object2 = {} 
function emptyObject(obj) {
    if( Object.keys(obj).length === 0 ) {
        return `object is empty`
    }else {
        return `object is not empty` 
    }
}
emptyObject(object2) // 'object is empty'
```
## The Use of ```Object.entries()``` Method with the ```Length``` Property
Just like ```Object.keys()``` method, the ```Object.entries()``` method also returns an array. However, ```Object.entries()``` method returns not just the property names of the object it applies to but also their values.
```javascript
let object3 = {
    x: 1,
    y: 2,
    z: 3,
}
Object.entries(object3) // [ ['x', 1], ['y', 2], ['z', 3] ]
```
You can use ```Object.entries()``` method with the ```length``` property to determine if the object the method applies to is empty or not. For instance:
```javascript
let object4 = {
    property1: 10,
    property2: 20,
}  
function emptyObject(obj) { 
    if( Object.entries(obj).length === 0 ) { 
        return `object is empty` 
    }else { 
        return `object is not empty`  
    } 
} 
emptyObject(object4) // 'object is not empty'
```

## Conclusion
Checking if an object is empty can be tricky, especially if you are unaware of the right method to use. The two methods that this article provides in checking if an object is empty or not apply to any scenario.