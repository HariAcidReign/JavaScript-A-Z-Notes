# Episode 7 : Scope and Lexical Environment

```
This is why JS is confusing (Case-1)

function a() {
    console.log(b); // surprisingly instead of printing undefined it prints 10. 
    //So somehow this b could access the b outside the fun. 
}

var b = 10;
a();

---------------------

Another case: (Case-2)

function a() {
  c();
  function c() {
  console.log(b); // when cursor comes here, it still prints out 10 somehow!!
  }
 }
 var b = 10;
 a();
 
 --------------------
 
 Another one (DJ KHALED!) (Case-3)
 
 function a() {
  var b = 10;
  c();
  function c() {
    console.log(b); //it prints the right value. How? See ans below Summary part
  }
 }
 
 a();
 console.log(b); // now when cursor comes here, it prints NOT DEFINED!

```

- This is the intuition behind **scope**
- Scope is directly dependent on the lexical environment
- **Lexical Environment** : local memory + lexical env of its parent
- Whenever an EC is created, a Lexical environment(LE) is also created and is referenced in the local EC(in memory space)
- Lexical means hierarchy. In the DJ KHALED (xD) code, function c is lexically inside function a. 
- So in EC of c(), variables and fun in c (none) + reference of lexical env of parent a() is there
- LE of a() in turn is its memory space + reference to LE of parent (Global EC)
- LE of Global EC points to *null*

 ```
    To summarize the above points:
    
    call_stack = [GEC, a(), c()]

    Now lets also assign the memory sections of each execution context in call_stack.

    c() = [[lexical environment pointer pointing to a()]]

    a() = [b:10, c:{}, [lexical environment pointer pointing to GEC]]

    GEC =  [a:{},[lexical_environment pointer pointing to null]]

 ```
  ### For case -3 
  - First JS engine searches for b in local mem of c(). Nothing is there. 
  - So it goes to the reference of Lexical env of parent a(). Here b = 10 is here. So it takes this value, goes back to c() and console prints it.
  - Had b not been in a(), then pointer would have gone to a()'s parent (Global EC and searched there). Had b not been there too, then it goes to LE of global's parent
  which is null. Now JS engine stops and says b is NOT DEFINED. 
  - **Lexical env of c = Local memory of c + LE of A + LE of Global**
  - This process of going one by one to parent and checking is called **scope chain**
 
  
  







