# Episode 10 : Closures in JS

### Important Interview Question

**Closure :** Function bundled together with its lexical environment/scope.

```
JS is a weird language. You can pass functions as parameters to another function, assign a variable to an entire function, or even return a function.
eg:

function x() {
  var a = 7;
  function y() {
  console.log(a);
}
  return y;   // instead of y();
}
var z = x();
console.log(z);  // value of z is entire code of function y.

```

When functions are returned from another fun, they still maintain their lexical
scope.

- When y is returned, not only is the fun returned but the entire closure (fun
  y + its lexical scope) is returned and put inside z. So when z is used
  somewhere else in program, it still remembers var a inside x()
- Closure is a very powerful concept of JS, just because this function remembers
  things even if they are not in their lexical scope

### Uses of Closure

Module Design Pattern, Currying, Functions like once(fun that can be run only
once), memoize, maintaining state in async world, setTimeout, iterators...
