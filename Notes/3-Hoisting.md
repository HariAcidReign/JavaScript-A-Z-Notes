# Episode 3 : Hoisting

```
// code example 1

var x = 7;

function getName(){
    console.log("Namaste JavaScript");
}

getName();
console.log(x);

```

Output:

> Namaste JavaScript

> 7

```
// code example 2

getName();      // in most languages, both lines which are above their declaration will give error. Not in JS though.
console.log(x);

var x = 7;

function getName(){
    console.log("Namaste JavaScript");
}

```

Output:

> Namaste JavaScript

> undefined

```
// code example 3

getName();
console.log(x);

function getName(){
    console.log("Namaste JavaScript");
}

```

Output:

> Namaste JavaScript

> Error: x is not defined // note that not defined here and "undefined" in
> sample 2 are totally different.

- Not defined: We have not initialised the value for variable anywhere in the
  entire code and in memory space.
- Undefined: It is a placeholder that is assigned to a variable by the
  Javascript Engine until the variable is assigned with some other value.

**Hoisting** is a concept which enables us to extract values of variables and
functions even before initialising/assigning value without getting _error_

```

// code example 4

function getName(){
    console.log("Namaste JavaScript");
}

console.log(getName)


```

Output:

> f getName(){

      console.log("Namaste JavaScript);

}

```

// code example 5

getName();
console.log(x);
console.log(getName)

var x = 7;

function getName(){
    console.log("Namaste JavaScript");
}

```

Output:

> Namaste JavaScript

> undefined

> f getName(){

      console.log("Namaste JavaScript);

}

```
// code example 6

console.log(getName)

var getName = function () {
    console.log("Namaste JavaScript");
}

var getName = () => {  // use fat arrow function
    console.log("Namaste JavaScript");
}

```

Output:

> undefined //it is because they behave as variable and not function.

---

**REASON OF WEIRDNESS**

- The answer lies in the Global Exection Context. In the memory phase, the
  variables will be initialized as _undefined_ and functions will get the whole
  function code in their memory.

- This is the reason why we are getting these outputs.
