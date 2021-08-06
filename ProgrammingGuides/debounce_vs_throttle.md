# Debounce vs Throttle

* Both are used to limit the number of times a function can execute
* When users can decide the execution rate of some functions, the developer may want a mechanism to restrict the number of times users can execute functions

> Debounce: batch a brust of events and trigger a single event

> Throttle: control the flow of events and trigger an event only once in a specified time interval

## Main difference
* Throttling executes the function at a **regular interval**
* Debouncing executes the function only after some **cooling period**

## Debounce explanation
* Suppose the user can type 1 letter per 100ms, but the requested function need 500ms to execute
* Before the function finished, the naive implementation will fire out 5 requests, which are redundant
* We can call the requested function once after the user have completed his typing
* So we can set a threshold, let's say 200ms, if the user **doesn't** type for 200ms, we will fire out a request

```javascript
let timerId;

let debounceFunction = (func, delay) => {
    clearTimeout(timerId);
    timerId = setTimeout(func, delay);
}
```

## Throttling explanation
* No matter how many times the user fires the event, the attached function will be executed only once in a given time interval
* When the user type the first letter, we can schedule the requested function to be executed after 500ms
* So every 1s (500ms + 500ms), the function will be executed once

```javascript
let timerId;
// Throttle function: input as function which needs to be throttled and delay is the time interval in milliseconds
let throttlingFunction = (func, delay) => {
    // If setTimeout is already scheduled, no need to do anything
    if (timerId) {
        return;
    }

    // Schedule a setTimeout after delay seconds
    timerId = setTimeout(() => {
        func();

        // Once setTimeout function execution is finished, timerId = undefined so that in
        // the next scroll event function execution can be scheduled
        timerId = undefined;
    }, delay)
}
```

## Reference
[Debouncing and Throttling in JavaScript](https://www.telerik.com/blogs/debouncing-and-throttling-in-javascript)
