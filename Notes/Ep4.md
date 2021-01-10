# Episode 4 : Functions and Variable Environments

```
var x = 1;
a();
b();   // we are calling the functions before defining them. This will work properly, as seen in Hoisting (Ep3)
console.log(x);

function a() {
  var x = 10;
  console.log(x);
}


function b() {
  var x = 100;
  console.log(x);
}

```

Outputs:

> 10

> 100

> 1

