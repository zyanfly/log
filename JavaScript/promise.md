### 基本实现
Promise是一个对象，对象能够保存状态，所以promise能做callback函数不能做的事情  
Promise最大的好处就是在异步执行的流程中，把执行代码和处理结果的代码清晰的分离了。  
Promise有以下三个状态：
- __pending__（进行中、未完成）
- __fulfilled__（已成功）
- __rejected__（已失败）
```js
// promise接受一个函数作为参数，函数接受两个回调函数为参数，第一个resolve为成功的回调函数，第二个为失败的回调函数
const http = new Promise((resolve, reject) => {
    http.get('url',data)
    .success(res => {
        // 正确返回数据
        resolve(res);
    })
    .error(err => {
        // 请求发生错误
        reject(err);
    })
})
http.then(res => {// 成功后的回调函数
    console.log(res);
},error => { // 失败后的回调函数
    console.log(error)
})
```
### Promis.all(Array<promise>)
在promise应用中有可能会出现这样的需求，某些操作需要等到多个promise执行完毕后再执行  
比如在一个页面发送多个请求后关闭loading动画  
这种情况就需要用到promise的all函数  
只有所有promise返回才会触发all的than回调
```js
Promise.all([promise1, promise2, promise3])
.than(res => {
    /*
    * 处理返回的res结果
    * res类型为数组，分别是参数中promise的返回内容[res1, res2, res3]
    */
    res1 = res[0];
    res2 = res[1];
    res3 = res[2];
})
```
### promise.race(Array<promise>)

```
// Promise.race为竞争关系，返回第一个异步执行完成的内容
Promise.race([promise1, promise2, promise3])
.than(res => {
    // 第一个执行完成者
})
```

