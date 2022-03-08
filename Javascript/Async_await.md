[Using Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
[Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
[In depth: Microtasks and the JavaScript runtime environment](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide/In_depth#tasks_vs_microtasks)


### Promises
A Promise is an object representing the eventual completion or failure of an asynchronous operation.

#### short for 
 `catch(failureCallback)` is short for `then(null, failureCallback)`

#### tip
Important: Always return results, otherwise callbacks won't catch the result of a previous promise (with arrow functions () => x is short for () => { return x; }).

## Chaining after a catch
It's possible to chain after a failure, i.e. a `catch`, which is useful to accomplish new actions even after an action failed in the chain. Read the following example:
```js
new Promise((resolve, reject) => {
    console.log('Initial');

    resolve();
})
.then(() => {
    throw new Error('Something failed');

    console.log('Do this');
})
.catch(() => {
    console.error('Do that');
})
.then(() => {
    console.log('Do this, no matter what happened before');
});
```
This will output the following text:
```console
Initial
Do that
Do this, no matter what happened before
```

---

### async
So the async keyword is added to functions to tell them to return a promise rather than directly returning the value.

###
await only works inside async functions within regular JavaScript code, however it can be used on its own with JavaScript modules.

### [Awaiting a Promise.all()](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await#awaiting_a_promise.all)

