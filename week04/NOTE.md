# 每周总结可以写在这里

```
async function afoo(){
    console.log("-2")


    await new Promise(resolve => resolve());
    console.log("-1")
}


new Promise(resolve => (console.log("0"), resolve()))
    .then(()=>(
        console.log("1"), 
        new Promise(resolve => resolve())
            .then(() => console.log("1.5")) ));


setTimeout(function(){
    console.log("2");
    
    new Promise(resolve => resolve()) .then(console.log("3"))


}, 0)
console.log("4");
console.log("5");
afoo()
```

所有的JS代码都是一个微任务，只是哪些微任务构成了一个宏任务；执行在JS引擎里的就是微任务，执行在JS引擎之外的就是宏任务，循环宏任务的工作就是事件循环。

resolve的执行，产生了一个额外的微任务，添加在微任务队列的最后。

setTimeout、setInterval 这种 JS 的宿主浏览器提供的 API， 执行时会开启新的宏任务。 而 Promise 是 JS 本身自带的 API，这种就是微任务。