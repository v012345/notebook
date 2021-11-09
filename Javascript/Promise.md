```Javascript
doSomething()
.then(function(result) {
  return doSomethingElse(result);
})
.then(function(newResult) {
  return doThirdThing(newResult);
})
.then(function(finalResult) {
  console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);
```
上面的`.catch(failureCallback)`是`.then(null,failureCallback)`的简写

如果出现异常,浏览器会顺着链去找`.catch`或者`.then`中的`rejected`方法

### 这里有用来`async/await`
> 这里简单说一下应用,原理是什么,我还没看到,应该就是字面意思,`async`声明表示这个函数中可能存在异步操作,`await`就是等待这个函数中的异步操作返回结果后,再向下执行
