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

## 使用中发现
`.then`的话,如果你不写`return`,也不抛错的话,会默认返回一个**成功**的`Promise`对象,如果我写
```javascript
return new Promise();
```
那么下一个`.then`会根据这个`Promise`的状态干活,如果`Promise`不指明状态,那么就停在这个`.then`上.