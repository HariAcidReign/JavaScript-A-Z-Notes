# Episode 15 : Callbacks and Event Listeners

**Callback Function :** Functions are first class citizens (see prev lecture) ie. take a fun A and pass it to another fun B. Here, A is a callback function
- JS is a synchronous and singlethreaded language. But due to callbacks, we can do async things in JS. 

> setTimeout(function () {}, 1000) -> here the anony function is a callback function as it is passed to setT and called sometime later in code after certain time (here 1000ms).
- This is how we do async things. JS is a synch language, but it doesn't wait 1 sec for setT to finish before going to code below it. It stores the function, attaches timer
and goes down the code. 

```
setTimeout(function () {
  console.log("timer");
 }, 5000);
 
function x(y) {
  console.log("x");
  y();
}

x(function y() {
  console.log("y");
});
```

> x

> y

> timer

- In the call stack, first x and y are present. After completion, they go away and stack is empty. Then after 5 seconds(from beginning) anonymous suddenly pops up in stack ie. setTimeout
- All 3 functions are executed through call stack. If any operation blocks the call stack, its called **blocking the main thread**
- Say if x() takes 30 sec to run, then JS has to wait for it to finish as it has only 1 call stack/1 main thread. *Never block main thread*. 
- **Always use async for functions that take time eg. setTimeout**

**Event Listener** 

- When we create a button in HTML and attack a clickListener in JS :
```
in index.html

<button id="clickMe">Click Me!</button>

in index.js

document.getElementById("clickMe").addEventListener("click", function xyz(){ //when event click occurs, this callback function is called into callstack
    console.log("Button clicked");
});
```
 Suppose we want to increase count by 1 each time button clicked. 
 - Use global variable (not good as anyone can change it)
 
 ```
 let count = 0;
 document.getElementById("clickMe").addEventListener("click", function xyz(){ 
    console.log("Button clicked", ++count);
});
 ```
- Use closures for data abstraction

 ```
 function attachEventList() {  //creating new fun for closure
    let count = 0;
    document.getElementById("clickMe").addEventListener("click", function xyz(){ 
    console.log("Button clicked", ++count);  //now callback fun forms closure with outer scope(count)
});
}
attachEventList();
```

#### Garbage Collection and removeEventListeners 
- Event listeners are heavy as they form closures. So even when call stack is empty, EventListener won't free up memory allocated to *count* as it doesn't know
when it may need *count* again. 
- **So we remove event listeners when we don't need them (garbage collected)**
- onClick, onHover, onScroll all in a page can slow it down heavily. 
