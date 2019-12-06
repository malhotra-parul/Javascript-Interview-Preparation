# Interview Questions for Javascript

1. What is _CallBack Hell_? How can we avoid callback hell in Node JS?

Callback functions are functions passed as arguments to another function. Callbacks are used to make Javascript calls asynchronous in nature. By default, Javascript will run the code line by line from top to bottom. However, when it encounters a function passed as an argument to another function i.e. a **Callback**, it offloads the execution part to the hosting environment(which can be a browser or nodeJs) while it itself continues with synchronous execution.

**Callback Hell** occurs when multiple callbacks within a callback is used. This leads to a pyramid shaped structure which is very difficult to read and understand.

A simple example would be -

```
    const button = document.getElementById("button");
    console.log("First statement");
    button.addEventListener("click", () => {
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
    });
    console.log("Last statement");
```

As can be seen in the snippet above, there is a function eventListener calling another function which in turns call the third function, making the code very difficult to understand. This is called as **Callback Hell**.

To avoid Callback Hell we can use below methods -

- Use modules and name functions well - If we name all the functions seperately and use their variable names instead, we can avoid Callback Hell upto a larger extent.
  Example -

```
const button = document.getElementById("button");
    console.log("First statement");
    button.addEventListener("click", trackUser);
    function trackUser() {
      navigator.geolocation.getCurrentPosition(position, error);
    }
    var position = (posData) => {
          setTimeout(() => {
            console.log(posData);
          }, 4000);
        };

    var error = (error) => {
        console.log(error);
    };

    console.log("Last statement");
```

Here, we have created functions seperately and used variable names instead.

- Use Promises -
  Using promises, we have wrapped getCurrentPosition and setTimeout into two promises and used promise chaining to resolve both of them sequentially.

```
const getPosition = () => {
        const promise = new Promise((resolve, reject)=>{
            navigator.geolocation.getCurrentPosition((success) => {
                resolve(success);
            }, (error) => {
            });
        });
        return promise;
    };
    const setTimer = function(duration) {
      const promise = new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Done!");
        }, duration);
      });
      return promise;
    };
    const button = document.getElementById("button");
    console.log("First statement");
    button.addEventListener("click", trackUser);
    function trackUser() {
        var posData ;
        getPosition()
            .then((positionData)=>{
            posData = positionData;
            return setTimer(2000);
        })
            .then((data)=>{
            console.log(data, posData);
            });
    };
    console.log("Last statement");
```

- Use Async/await - Using Async, Await we can further reduce the complexity of the code, making it much easier to understand.

```
    const getPosition = () => {
      const promise = new Promise((resolve, reject) => {
        navigator.geolocation.getCurrentPosition(
          success => {
            resolve(success);
          },
          error => {
            reject(error);
          }
        );
      });
      return promise;
    };
    const setTimer = function(duration) {
      const promise = new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve("Done!");
        }, duration);
      });
      return promise;
    };
    const button = document.getElementById("button");
    console.log("First statement");
    button.addEventListener("click", trackUser);
    async function trackUser() {
      let posData;
      let timerData;
      try {
        posData = await getPosition();
        timerData = await setTimer(2000);
      } catch (error) {
        console.log(error);
      }
      console.log(posData, timerData);
    }
    console.log("Last statement");
```

2. How do we change Node versions instantly without _reinstalling_ Node JS?

3) How can you build large scalable applications using Node JS? When not to use Node JS? Explain with a scenario.

4) Explain about _EventEmitter_ in Node JS withan Example Code.

5) Explain about _stub_ with an example code.
