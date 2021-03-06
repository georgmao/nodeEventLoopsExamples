# nodeEventLoopsExamples


## Introduction
NodeJS utilizes an asynchronous programming model, via the Event Loop. However, sometimes it is necessary to invoke operations synchronously in sequence or parallel. This sample demostrates two approaches to this.

This project is [SAM](https://github.com/awslabs/aws-sam-local/) enabled! Just run it like this:

```bash
sam local invoke AsyncTest -e "event.json"
sam local invoke promiseTest -e "event.json"
```

## A Promise Example
First, is by issuing Promises and fullfilling them when the Async calls complete. A fully functional example is shown in **promiseExample.js**.
Instead of issuing callbacks, we create a Promise then call the .then() operator when the promise is ready.

```node
var url = docClient.query(params).promise();
```

```node
url.then(function (someResult){
    // Do something here
});
```

Second, is by using a 3rd party library  [async](https://caolan.github.io/async/). This library allows calls occur in series, parallel, or waterfall mode by issuing Callbacks. A fully functional examle is show in **asyncTests.js**

## A Callback Example

```node
async.series([
    function(callback){
        console.log('ji');
        callback(null, 'one');
    },
    function(callback){
        console.log('adsf');
        callback(null, 'two');
    }],
    function(err, results){
        console.log(results);
    }
);
```

## Resources

- **asyncTests.js** - NodeJS Based Lambda function demostrates how to use Callbacks to control the Event loop
- **promiseExample.js** - NodeJS Based Lambda function demostrates how to use Promises to control the Event loop