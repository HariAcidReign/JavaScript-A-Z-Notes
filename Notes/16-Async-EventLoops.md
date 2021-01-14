# Episode 16 : Asynchronous JS and Event Loops

> Note that call stack will execeute any execeution context which enters it. Time, tide and JS waits for none. TLDR : Call stack has no timer

**Browser has JS Engine which has Call Stack which has Global exec context, local exec context etc**
- But browser has many other *superpowers* - Local storage space, Timer, place to enter URL, Bluetooth access, Geolocation access and so on
- Now JS needs some way to connect the callstack with all these superpowers. 

