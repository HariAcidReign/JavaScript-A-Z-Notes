# Episode 17 : Trust Issues with setTimeout() 

(Episode number mixup. This is the actual 17th episode)

```
console.log("Start");

setTimeout(function cb() {
  console.log("Callback");
 }, 5000);
 
 console.log("End");
 
setTimeout sometimes does not exactly guarantee that the callback method will be called exactly after 5s. 
Maybe 6,7 or even 10! It all depends on callstack
```

While execution of program 

- First GEC is created and pushed in callstack. 
- Start is printed in console
- When setT is seen, callback method is registered into webapi's env. And timer is attached to it and started. cb waits for its turn to be execeuted once timer expires.
But JS waits for none. Goes to next line
- End is printed in console. 
- After "End" suppose we have 1 million lines of code that runs for 10 sec(say). So GEC won't pop out of stack. It runs all the code for 10 sec. 
- But in the background, the timer runs for 5s. While callstack runs the 1M line of code, this timer has already expired and cb fun has been pushed to Callback queue.
- Event loop keeps checking if callstack is empty or not. But here GEC is still in stack so cb can't be popped from callback Q and pushed to CallStack. 
** Though setT is only for 5s, it waits for 10s until callstack is empty before it can execute**(When GEC popped after 10sec, cb() is pushed into call stack and 
**immediately executed** (Whatever is pushed to callstack is executed instantly)
- This is called as the **Concurrency model of JS**. This is the logic behind setT's trust issues

### The First rule of JavaScript
- **Do not block the main thread** (as JS is a single threaded(only 1 callstack) language)

- This raises a question. *Why not add more call stacks and make it multithreaded?* 
- JS is a synch single threaded language. And thats its beauty. With just 1 thread it runs all pieces of code there. It becomes kind of an interpreter lang,
and runs code very fast inside browser (no need to wait for code to be compiled) (JIT - Just in time compilation). And there are still ways to do async operations as well. 

### Now what if the timeout = 0sec
```
console.log("Start");

setTimeout(function cb() {
  console.log("Callback");
 }, 0);
 
 console.log("End");
 
```
- Even though timer = 0s, the cb() has to go through the queue. Registers calback in webapi's env , moves to callback queue, and execute once callstack is empty

> Start

> End

> Callback

- This method of putting timer = 0, can be used to defer a less imp fun by a little so the more important fun (here printing "End") can take place 
