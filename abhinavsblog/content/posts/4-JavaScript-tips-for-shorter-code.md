---
title: "4 JavaScript Tips for Shorter Code"
date: 2021-11-21T16:09:31+05:30
---

There are plenty of tips which can be followed to make the JavaScript code shorter as well less complicated. I will share four of such tips which have reduced the effort and development time for me a lot while coding.

# 1. Short Circuiting
This can be used when you’ll have to use a simple if condition.
```js
if( x == 0 ){
  foo()
}
```
Short circuiting can be achieved by using && operator. Code after && won’t be executed if the condition before && evaluates to false.
```js
x == 0 && foo()
```
This can be chained to replace multiple if statements
```js
x == 0 && y == 0 && foo()
```
# 2. Check if objects exist using ? operator
This is really helpful if you are dealing with scenarios like API calls or with objects of which you aren’t certain whether it or its keys are initialised.
Consider an object studentObject with a key ‘name’ with value an object with key ‘firstName’. Directly accessing the key value using ‘studentObject.name.firstName’ might throw error . One way to evaluate whether the key exists is using nested if conditions.
```js
const studentObject = {
  name : {
    firstName : 'Joe'
  }
}
if(studentObject.name){
  if(studentObject.name.firstName){
    console.log('student First name exists')
  }
}
```
This can be made shorter using ‘?’ operator. If studentObject.name do not exist it will evaluate to false.
```js
const studentObject = {
  name : {
    firstName : 'Joe'
  }
}
if(studentObject.name?.firstName){
  console.log('student First name exists')
}
```
Edit : Node has only limited support for optional chaining operator.
# 3. Using Nullish coalescing operator (??)
Ternary operator already makes the code short as compared to if else statement. It’s handy if the block of code to be executed is small.
```js
const foo = () => {
  return studentObject.name?.firstName ? 
    studentObject.name.firstName : 
    'firstName do not exist'
}
console.log(foo())
```
In cases where you have to return the operand to the left of ‘?’, you can use the ‘??’ operator to make the code even shorter.
```js
const foo = () => {
  return studentObject.name?.firstName ?? 
  'firstName do not exist'
}
console.log(foo())
```
# 4. Terminating the function instead of if else nesting
consider the below function which checks the value of ‘x’
```js
const foo = () => {
  if(x<1){
    return 'x is less than 1'
  }else{
    if(x > 1){
      return 'x is greater than 1'
    }else{
      return 'x is equal to 1'
    }
  }
}
```
This if else nesting can be made less complicated by removing else conditions, as a return statement will stop code execution and return the function.
```js
const foo = () => {
  if(x<1){
    return 'less than 1'
  }
  if(x>1){
    return 'x is greater than 1'
  }
  return 'x is equal to 1'
}
```

# A good code need not be short
Preference must be given for readability over making the code shorter. In some cases debugging the code would be quite hard especially if the code is maintained by multiple developers.
Short-circuiting is a feature of expression evaluation. In this case, you're using that feature to actually execute code; in other words, a side-effect of the expression is that it executes code.
There are two problems with this idea:
1. it encourages writing even more complex expressions simply for their side-effects, eventually becoming a maintenance nightmare.
2. it's doesn't execute the actual code any faster than the explicit (if) form.
A good rule of thumb: explicit > implicit