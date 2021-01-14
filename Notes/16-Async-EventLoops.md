# Episode 16 : Asynchronous JS and Event Loops

> Note that call stack will execeute any execeution context which enters it. Time, tide and JS waits for none. TLDR : Call stack has no timer

**Browser has JS Engine which has Call Stack which has Global exec context, local exec context etc**
- But browser has many other *superpowers* - Local storage space, Timer, place to enter URL, Bluetooth access, Geolocation access and so on
- Now JS needs some way to connect the callstack with all these superpowers. This is done using **Web APIs**

### WebAPIs
None of the below are part of Javascript! These are extra superpowers that browser has. Browser gives access to JS callstack to use these powers.
> setTimeout(), DOM APIs, fetch(), localstorage, console (yes, even console.log is not JS!!), location and so many more..

- setTimeout() : Timer function 
- DOM APIs : eg.Document.xxxx ; Used to access HTML <html><script><body>..... DOM tree. (Document Object Manipulation)
- fetch() : Used to make connection with external servers eg. Netflix servers etc.

We get all these inside call stack through *global object* ie. **window**
- Use window keyword like : window.setTimeout(), window.localstorage, window.console.log() to log something inside console. 
- As window is global obj, and all the above functions are present in global object, we don't explicity write *window* but it is implied

### Workflow

```
// First a GEC is created and put inside call stack. 
console.log("Start"); // this calls the console web api (through window) which in turn actually modifies values in console. 

setTimeout(function cb() {  //this calls the setT web api which gives access to timer feature. It stores the callback cb() and starts timer.  
  console.log("Callback");
 }, 5000);
 
console.log("End"); // calls console api and logs in console window. After this GEC pops from call stack. 

```
- While all this is happening, the timer is constantly ticking. After it becomes 0, the callback cb() has to run. 
- Now we need this cb to go into call stack. Only then will it be executed. For this we need **event loop and Callback queue**

### Event Loops and Callback Queue
- cb() cannot simply directly go to callstack to be execeuted. It goes through the callback queue when timer expires. 
- Event loop checks the callback queue, and if it has element puts it into call stack. It is a *gate keeper*. 
- Now cb() in callstack is run. Console API is used and log printed

Final console output:
 
> Start

> End

> Callback

### Same happens for any other event as well (Click, Hover etc). This is the basic workflow.

```
console.log("Start"); 
document. getElementById("btn").addEventListener("click", function cb() { // cb() registered inside webapi environment and event(click) attached to it. ie.
// REGISTERING CALLBACK AND ATTACHING EVENT TO IT. 
  console.log("Callback");
});
 
console.log("End"); // calls console api and logs in console window. After this GEC pops from call stack. 

```
In above code, even after console prints "Start" and "End" and pops GEC out, **the eventListener stays in webapi env**(with hope that user may click it
some day) until explicitly removed, or the browser is closed.

### Why need callback queue? 
- Why can't event loop directly take cb() and put it in callstack?  Suppose user clciks button x6 times. So 6 cb() are put inside callback queue.
- Event loop sees if call stack is empty/has space and whether callback queue is not empty(6 elements here). 
- Elements of callback queue popped off, put in callstack, executed and then popped off from call stack.

### fetch() works a bit different than the rest
```
console.log("Start"); // this calls the console web api (through window) which in turn actually modifies values in console. 

setTimeout(function cbT() { 
  console.log("CB Timeout");
 }, 5000);
 
 fetch("https://api.netflix.com").then(function cbF() {
  console.log("CB Netflix");
 });
 
console.log("End"); 

```
- Same steps for everything before fetch() in above code. 
- fetch registers cbF into webapi environment along with existing cbT. 
- cbT is waiting for 5000ms to end so that it can be put inside callback queue. cbF is waiting for data to be returned from Netflix servers. 
- fetch requests data from Netflix servers, and get data back and now cbF ready to be executed. 
**We have something called a Microtask Queue**
- It is exactly same as Callback queue, but it has higher priority. Functions in Microtask Q are executed earlier than Callback Q. 
- cbF goes inside the Microtask Q and not callback Q. Once call stack is empty, Event loop gives chance for elements in **both** Microtask Queue and 
Callback Queue to enter Call Stack. 

- In console, first *Start* and *End* are printed in console. First cbF goes in callstack and "CB Netflix" is printed. cbF popped from callstack
- Next cbT is removed from callback Q, put in Call Stack, "CB Timeout" is printed, and cbT removed from callstack.

### What enters the Microtask Queue ?
- All the callback functions that come through *promises* go in microtask Q. 
- **Mutation Observer :** Keeps on checking whether there is mutation in DOM tree or not, and if there, then it execeutes some callback function. 
- Callback functions that come through *promises and mutation observer* go inside Microtask Queue. 
- All the rest goes inside **Callback Queue aka. Task Queue**

- If the task in microtask Queue keeps creating new tasks in the queue, element in callback queue never gets chance to be run. This is called **starvation**

### Some Important Questions 

1. **When does the event loop actually start ? -** Event loop, as the name suggests, is a single-thread, loop that is *almost infinite*. It's always running and doing its job.

2. **Are only asynchronous web api callbacks are registered in web api environment? -** YES, the synchronous callback functions like what we pass inside map, filter and reduce aren't registered in the Web API environment. It's just those async callback functions which go through all this.

3. **Does the web API environment stores only the callback function and pushes the same callback to queue/microtask queue? -** Yes, the callback functions are stored, and a reference is scheduled in the queues. Moreover, in the case of event listeners(for example click handlers), the original callbacks stay in the web API environment forever, that's why it's adviced to explicitly remove the listeners when not in use so that the garbage collector does its job.

4. **How does it matter if we delay for setTimeout would be 0ms. Then callback will move to queue without any wait ? -** No, there are trust issues with setTimeout() 😅. The callback function needs to wait until the Call Stack is empty. So the 0 ms callback might have to wait for 100ms also if the stack is busy.
