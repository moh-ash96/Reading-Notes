# Node.js

**Node.js** is an:
* Event based.
* non-blocking.
* Asyncronous I/O runtime that uses JavaScript engine and libuv library.

*Event based*, *non blocking*, *asyncronous* mean that everything that happens in **Node** is in reaction to an *event*; that means when a new request comes in, the server will start processing it, if it then encounters a blocking I/O operation, instead of waiting for it to complete, it will register a callback before cotinuing to process the next event, When the *I/O operation* has finished another kind of event, the server will execute the callback and continue working on the original request. Under the hood, Node uses the *libuv* library to implement this asynchronous (that is, non-blocking) behavior.

**Node’s** execution model causes the server very little overhead, and consequently it’s capable of handling a large number of simultaneous connections. The traditional approach to scaling a **Node app** is to clone it and have the cloned instances share the workload. Node.js even has a built-in module to help you implement a cloning strategy on a single server.

Node's execution model:

![](https://uploads.sitepoint.com/wp-content/uploads/2012/10/1516152673node_event_loop.png)

**Node.js** best suited to build applications that require *real-time* interaction and collaboration, such as chat apps and applications like google docs.

The best thing about **Node.js** is that it uses *JavaScript* on a web server, and that means you can do everything in the same language, which make you more productive and makes it easier to share code between the server and the client.

Also a good thing about **Node.js** that it uses *JSON*, which is the most important data exchange format on the web, and is ideally suited for consumption by a JavaScript program.
