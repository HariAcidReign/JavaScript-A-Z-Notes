# Episode 5: Window and this keyword

### Everywhere JS is run, it is done with a JS execution engine. For Chrome: v8

- Shortest JS program is nothing but an Empty JS file
- Even for this program, JS engine does a lot behind the scenes
- It creates the GEC, the "window" and the *this* variable
- Window is a big global object that has a lot of functions and variables. All of these can be accessed from anywhere in the program
- *this* points to *window*
> this === window -> true (at global level)
```
var a = 10;      // not inside any fun. So global object
function b() {    // this fun not inside any function. So global.
  var x = 5;    // not global
 }
console.log(window.a); //gives us "a" value
console.log(this.a); //this points to window so it returns "a" value
console.log(a); //also gives same "a" value. (if we dont put any . in front of variable, it **assumes variable is in global space**
console.log(x); // x is not defined. (tries to find x inside global space, but it isn't there) 
```
- Global space is anything in JS which isn't inside a function. All these global objects will be present inside the windows schema. But non globals ones won't be there (here, x)
- When a GEC is made, *this* is also created with it (even for functional(local) EC). Global object provided by the browser engine is the window, so *this* points to window.
