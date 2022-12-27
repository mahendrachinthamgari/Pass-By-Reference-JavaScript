# Importance of Error Handling in Promises

>Error Handling is very important while dealing with promises.

We know that a promise has to be resolved or rejected. So handling rejected promises is as important as handling resolved promises.

If we ignore the errors in promises we may get into big trouble, because we don't know what is happening in the code and we may not able to get the desired output and sometimes we may not understand the error.

If we handle the errors properly, we can make the errors more human-redable errors. So that we can easily the resolve the errors.

> Promise chains are gereat at error handling. 

### How to handle errors in promises

Errors can be handled in the promises by using `.catch`. If any promise has been rejected, then the control will jumps to the closest rejection handler i.e., `.catch`.  

Consider an example:

```
fetch('https://examplepromise123.com')
    .then((resopnse) => {
        return resopnse.json();
    })
    .then((data) => {
        console.log(data);
    })
    .catch((err) => {
        console.error(err);
    })
```

Output of the above code: 
```
TypeError: fetch failed
    at Object.fetch (node:internal/deps/undici/undici:14294:11)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5) {
  cause: Error: getaddrinfo ENOTFOUND examplepromise123.com
      at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:107:26) {
    errno: -3008,
    code: 'ENOTFOUND',
    syscall: 'getaddrinfo',
    hostname: 'examplepromise123.com'
  }
}
```
In the above example we are trying to fetch the data from a site that is not valid. As we know that fetch will return a promise, since the site url is not valid, the fetch will return a rejected promise. Whenever the promise is rejected, the controll will jump to the closest rejection handler, `.catch`, it  consoles an error. 

If any promise got rejected above the `.catch` then all the `.then` blocks will not executed above `.catch`

Consider anothe example:

```
firstRequest()
    .then((response) => {
        return secondRequest(response);
    })
    .then((nextResponse) => {
        return thirdRequest(nextResponse);
    })
    .then((finalResponse) => {
        console.log('Final response: ' + finalResponse);
    })
    .catch(failureCallback);

```
In the above example, when the promises are chained, whenever a promise gets rejected, than the controll jumps to the `.catch` block and the `.then` blocks above the `.catch` block will not be executed and if there are any `.then` blocks present under the `.catch` block will continue to execute.

Example: 
```
fetch('https://examplepromise123.com')
    .then((resopnse) => {
        return resopnse.json();
    })
    .then((data) => {
        console.log(data);
    })
    .catch((err) => {
        console.error(err);
    })
    .then(() => {
        consloe.log('What ever happens this will execute');
    })
```
Output of the above code:
```
TypeError: fetch failed
    at Object.fetch (node:internal/deps/undici/undici:14294:11)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5) {
  cause: Error: getaddrinfo ENOTFOUND examplepromise123.com
      at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:107:26) {
    errno: -3008,
    code: 'ENOTFOUND',
    syscall: 'getaddrinfo',
    hostname: 'examplepromise123.com'
  }
}
What ever happens this will execute
```

There is a `.then` block below the `.catch` block, it means that `.catch` is not respnsible for the `.then` blocks which are present under the `.catch` block. So no matter what happens above the `.catch` block, the below `.then` blocks will gets executed `.catch` block handles the rejected promises above the `.catch` block.