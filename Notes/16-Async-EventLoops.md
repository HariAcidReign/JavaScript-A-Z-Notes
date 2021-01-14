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




