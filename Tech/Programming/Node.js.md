A thread in simple words is time and resources the CPU gives to execute a small unit of instructions. With that said, the server attends multiple requests at once, one per thread (also called thread-per-request model).

Javascript server-side wasn't new in the early 2000s, there were a few implementations ontop of the Java Virtual Machine like RingoJS and AppEngineJS, based on thread-per-request model. But at the time, it was not possible to concurrently handle 10,000 clients connections on a single server machine because javascript is single threaded.

Node.js is a server-side platform built on Google Chrome's Javascript Engine (V8 Engine) which compiles Javascript code into Machine code.
Node.js tt's not a Framework, it's not a Library, it's a runtime environment.
```
// Importing native http module
const http = require('http');

// Creating a server instance where every call
// the message 'Hello World' is responded to the client
const server = http.createServer(function(request, response) {
  response.write('Hello World');
  response.end();
});

// Listening port 8080
server.listen(8080);
```

Node.js is non-blocking I/O, which means:
1. The main thread won't be blocked in I/O operations.
2. The server will keep attending requests.
3. We will be working with asynchronous code.

The Event Loop is the magic behind Node.js. In short terms, the Event Loop is literally an infinite loop and is the only thread available.