# Episode 14 : First class and Anonymous functions

(there is no Episode 13 idk why lol)

#### Function statement : Just your normal function definition 

```
function a() {
  console.log("a called");
}
a();

```

#### Function Expression : Assigning a function to a variable. Function acts like a value

```
var b = function() {
  console.log("b called");
}
b();

```

**Difference btw function statement and expression is Hoisting**
- You can put "a();" before "function a()" and it will still work. But putting "b();" before "var b = function()" throws a typeError.
- Why? During mem creation phase a is created in memory and function assigned to a. But b is created like a variable (b:undefined) and until code reaches the function() 
part, it is still undefined. So it cannot be called.

#### Function Declaration : Exactly same as function statement

#### Anonymous Function : A function without a name
- They don't have their own identity. So an anony function without code inside it results in an error. 
- Anony functions are used when functions are used as values eg. the code sample for function expression above

#### Named Function Expression : Same as Function Expression but function has a name instead of being anonymous
```
var b = function xyz() {
  console.log("b called");
}
b(); // prints "b called" properly
xyz(); // Throws ReferenceError:xyz is not defined.

```
> xyz function is not created in global scope. So it can't be called.

#### Parameters vs Arguments 
```
var b = function(param1, param2) {  // labels/identifiers that get the arg values 
  console.log("b called");
}
b(arg1, arg2); // arguments - values passed inside function call

```
#### First Class Function aka First Class Citizens
- You can pass functions inside a function as arguments(WOW!)

```
var b = function(param1) {
  console.log(param1); // prints " f() {} "
}
b(function(){
  
});

this can also be done:

var b = function(param1) {
  console.log(param1);
}
function xyz(){

}
b(xyz); // same thing as prev code

you can return a function from a function:

var b = function(param1) {
  return function() {
  
  }  
}
console.log(b()); //we log the entire fun within b. 

```
#### Arrow Functions (latest in ES6 (ECMAScript 2015) -> coming in future lecture

