# Interview Questions for Javascript 

1. What is _CallBack Hell_? How can we avoid callback hell in Node JS?

Callback functions are functions passed as arguments to another function. Callbacks are used to make Javascript calls asynchronous in nature. By default, Javascript will run the code line by line from top to bottom. However, when it encounters a function passed as an argument to another function i.e. a **Callback**, it offloads the execution part to the hosting environment(which can be a browser or nodeJs) while it itself continues with synchronous execution.

**Callback Hell** occurs when multiple callbacks within a callback is used. This leads to a pyramid shaped structure which is very difficult to read and understand.

A simple example would be -

```
    const button = document.getElementById("button");
    console.log("First statement");
    button.addEventListener("click", trackUser);
    function trackUser() {
      navigator.geolocation.getCurrentPosition(
        position => {
          setTimeout(() => {
            console.log(position);
          }, 4000);
        },
        err => {
          console.log(error);
        }
      );
    }
    console.log("Last statement");

```

2. How do we change Node versions instantly without _reinstalling_ Node JS?

3. How can you build large scalable applications using Node JS? When not to use Node JS? Explain with a scenario.

4. Explain about _EventEmitter_ in Node JS withan Example Code.

5. Explain about _stub_ with an example code.
