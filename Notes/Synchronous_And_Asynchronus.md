<h2>Synchronous</h2>
<p>Every Statement of code get executed one by one so basically a statement has to wait for earliar statement to get executed.<p>
 <h4>Example</h4>
 
 ```
    console.log("javascript");
    console.log("run");
    console.log("code");
  ```
  <p>It will print javascript first then run then code .<p>
 
  <h2>Asynchronous</h2>
  <p>It allow to program excuted immediatly without blocking the code unlike the synchronous method. it doesnot wait for earliear statment to get excuted first. </p>
  <p>Each task excuted completed independly.</p>
  
  ```
  console.log("javascript")
  setTimeOut(()=>{
      console.log("run");
      2000
  })
  console.log("code")
  
  ```
  <p>It will print javascript then code then run. </p>
  
  
  
