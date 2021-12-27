---
title: "Another 4 JavaScript Tips for Shorter Code"
date: 2021-11-28T17:17:20+05:30
---

This is a continuation to my earlier article : [4 JavaScript tips for shorter code](https://abhinavvp.com/posts/4-javascript-tips-for-shorter-code/)

---

## 1. Replace Switch or If-Else with key value pairs

The `switch` statement and `if-else` statement evaluates an expression and executes statements associated with that case. But as the number of cases increases the code grows as well.

```js
function returnDaySwitch(val) {
      switch (val) {
         case 1:
            return "It's monday";
         case 2:
            return "It's tuesday";
         case 3:
            return "It's wednesday";
         case 4:
            return "It's thursday";
         case 5:
            return "It's friday";
         case 6:
            return "It's saturday";
         case 7:
            return "It's sunday";
         default:
            return "Enter a value between 1 - 7";
      }
   }
function returnDayIfElse(val) {
    if(val==1){
        return "It's monday";
    }else if(val==2){
        return "It's tuesday";
    }else if(val==3){
        return "It's wednesday";
    }else if(val==4){
        return "It's thursday";
    }else if(val==5){
        return "It's friday";
    }else if(val==6){
        return "It's saturday";
    }else if(val==7){
        return "It's sunday";
    }else{
        return "Enter a value between 1 - 7";
    }
}
const day = 3;
console.log(returnDaySwitch(day)); //It's wednesday
console.log(returnDayIfElse(day)); //It's wednesday
```

This can be made simpler by using key-value pairs of an object. 
```js
function returnDayKeyValue(val) {
    const returnDayObject = {
        1: "It's monday",
        2: "It's tuesday",
        3: "It's wednesday",
        4: "It's thursday",
        5: "It's friday",
        6: "It's saturday",
        7: "It's sunday",
    }
    if(!returnDayObject[val]){
     return "Enter a value between 1 - 7";
    }
    return returnDayObject[val]
}
cosnt day = 3;
console.log(returnDayKeyValue(day)); //It's wednesday
```

## 2. Remove duplicate elements in an array

Duplicate elements in an array can be removed by Set constructor and spread syntax. Set constructor converts an array into a set which cannot have duplicate elements. Spread syntax can be used to convert the set object back to an array.

```js
const array = [1,2,2,3,4,5]
const uniq = [...new Set(array)];
console.log(uniq) // [1,2,3,4,5]
```

## 3. Computed property names

You cannot set object keys as variables directly. It will read the variable names as key names

```js
const key1 = "name";
const key2 = "age";
const student = {
    key1:"john Doe",
    key2:26
}
console.log(student)
//{ key1:"john Doe", key2:26 }
```

Starting with ECMAScript 2015, you can put an expression in brackets `[]`, that will be computed and used as the property name. 
```js
const key1 = "name";
const key2 = "age";
const student = {
    [key1]:"john Doe",
    [key2]:26
}
console.log(student)
//{ name:"john Doe", age:26 }
```

## 4. Prevent falsey value from evaluating to false

There are six falsey values in JavaScript: `undefined`, `null`, `NaN`, `0`, `""` (empty string), and `false`. A falsy value is something which evaluates to FALSE, for instance when checking a variable. There could be scenarios where you wont want any falsy value to evaluate to false.

```js
const number = 5;
if(number){
    console.log('The number exists')
}else{
    console.log('The number do not exist')
}
```

Will print `The number exists`. But

```js
const number = 0;
if(number){
    console.log('The number exists')
}else{
    console.log('The number do not exist')
}
```

Will print `The number do not exists`. This can be handled by giving an exception at the evaluation

```js
const number = null;
if(number===0?true:number){
    console.log('The number exists')
}else{
    console.log('The number do not exist')
}
```

Will print `The number exists`. `0` at the expression can be changed with any of the falsy values.