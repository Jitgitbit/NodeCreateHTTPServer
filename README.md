# NodeCreateHTTPServer.

Create an HTTP Server
Node was designed with back end development needs as a top priority. One of these needs is the ability to create web servers, computer processes that listen for requests from clients and return responses. A Node core module designed to meet these needs is the http module. This module contains functions which simplify interacting with HTTP and streamline receiving and responding to requests.

The http.createServer() method returns an instance of an http.server. An http.server has a method .listen() which causes the server to “listen” for incoming connections. When we run http.createServer() we pass in a custom callback function (often referred to as the requestListener). This callback function will be triggered once the server is listening and receives a request.

Let’s break down how the requestListener callback function works:

The function expects two arguments: a request object and a response object.
Each time a request to the server is made, Node will invoke the provided requestListener callback function, passing in the request and response objects of the incoming request.
Request and response objects come with a number of properties and methods of their own, and within the requestListener function, we can access information about the request via the request object passed in.
The requestListener is responsible for setting the response header and body.
The requestListener must signal that the interaction is complete by calling the response.end() method.
const http = require('http');

let requestListener = (request, response) => {
  response.writeHead(200, {'Content-Type': 'text/plain' });
  response.write('Hello World!\n');
  response.end();
};

const server = http.createServer(requestListener);

server.listen(3000);
Let’s walk through the above code:

We required in the http core module.
We created a server variable assigned to the return value of the http.createServer() method.
We invoked http.createServer() with our requestListener callback. This is similar to running the .on() of an EventEmitter: the requestListener will execute whenever an HTTP request is sent to the server on the correct port.
Within the requestListener callback, we make changes to the response object, response, so that it can send the appropriate information to the client sending the request. The status code 200 means that no errors were encountered. The header communicates that the file type is text, rather than something like audio or compressed data.
The last line starts the server with the port 3000. Every server on a given machine specifies a unique port so that traffic can be correctly routed.
You could run the above code on your local machine, and access it by visiting http://localhost:3000/ from your browser. “localhost” is used to refer to the same computer that’s running the current Node process.

In our example web server, we showed you a handful of the methods available on response objects. Be sure to check out the documentation to learn other methods and properties available on response and request objects.

Instructions
1.
In the example code earlier, we started a web server which only served the string ‘Hello World!\n’, now we want to serve some HTML. You can see the HTML for the website we’re going to serve in the myWebsite.html file. We’ve written a requestListener for you and required it into app.js. You can look at the code for requestListener in the callbackFile.js file.

Our requestListener expects to take in request and response objects (req and res). It invokes the fs.readFile() method with myWebsite.html. If there’s an error it will write the error while attempting to read the file to the response object, otherwise, it will write the contents of the file.

When you feel like you have a sense for the code base, move on to the next step!

Awesome work! You’ve learned a lot about Node.js including:

Node.js is a JavaScript runtime, an environment that allows us to execute our JavaScript code by converting it into something a computer can understand.
REPLs are processes that read, evaluate, print, and repeat (loop), and Node.js comes with its own REPL we can access in our terminal with the node command.
We run JavaScript programs with Node in the terminal by typing node followed by the file name (if we’re in the same directory) or the absolute path of the file.
Code can be organized into separate files, modules, and combined through requiring them where needed using the require() function.
In addition to core modules, modules included within the environment to efficiently perform common tasks, we can also create our own modules using module.exports and the require() function.
We can access NPM, a registry of hundreds of thousands of packages of re-usable code from other developers, directly through our terminal.
Node has an event-driven architecture.
We can make our own instances of the EventEmitter class and we can subscribe to listen for named events with the .on() method and emit events with the .emit() method.
Node uses an event loop which enables asynchronous actions to be handled in a non-blocking way by adding callback functions to a queue of tasks to be executed when the callstack is empty.
In order to handle errors during asynchronous operations, provided callback functions are expected to have an error as their first parameter.
Node allows for both output, data/feedback to a user provided by a computer, and input data/feedback to the computer provided by the user.
The Node fs core module is an API for interacting with the file system.
Streams allow us to read or write data piece by piece instead of all at once.
The Node http core module allows for easy creation of web servers, computer processes that listen for requests from clients and return responses.
Woah, that was a lot… And there’s even more to Node that we didn’t cover in this lesson, but don’t panic! Learning Node isn’t about memorizing every aspect of the environment. The best way to get comfortable with Node is just to practice making things in it. Your imagination is the limit! If you haven’t already, download Node on your local machine. You can start by recreating some of the programs you built in this lesson— put your own spin on a guessing game, for example. If you’re eager to build web application back-ends, we recommend you start learning the awesome Express.js web framework.

Great work! We’re excited to see what you build!

2.
It’s time to make the web server! In app.js, create a variable server and assign to it the value of invoking the http.createServer(). Remember, you’ll need to pass a callback function in as the argument to http.createServer(). We’ve already required in the function requestListener from the callbackFile.js file.

3.
Awesome! Now that we have the server we need it to start listening for incoming requests! We supplied a PORT variable at the top of app.js. Invoke the server.listen() method passing in PORT as the argument.

4.
Let’s get this server up and running! Type node app.js in the terminal and press enter. If everything worked, you should be able to navigate to http://localhost:4001 in the browser and see the rendered HTML.

Feel free to make changes and experiment. You can stop the server by typing controlc, make whatever changes you’d like, and then start the server by typing node app.js in the terminal again and pressing enter.
