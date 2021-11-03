## 正常表单提交下 disabled 的input为null
> 下面三种情况，在常规的发表单提交的情况，disabled 中的值是发不出去的，但是如果用js去取然后用ajax去发送，不知道行不行
```html
<input type="text" readonly value="readonly" />
<br />
<input type="text" disabled value="disabled" />
<br />
<input type="text" />
```
<input type="text" readonly value="readonly" />
<br />
<input type="text" disabled value="disabled" />
<br />
<input type="text" value="normal" />