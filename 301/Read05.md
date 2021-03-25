# HEROKU
Heroko is a cloud service that allows us to diploy our local server to be available world wide.
## Node.js
Firs we need to make our local server using node.js which is a JavaScript file the containes the code to make that server in the following steps:
* Create a javascript file and name it server.js
* Add the following lines of code:
    ```
    var http = require("http");

    http.createServer(function(request, response) {
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("It's alive!");
    response.end();
    }).listen(3000);
    ```
* Check if it is working by adding this to terminal
    ```
    node server.js
    ```
* Make it world wide using heroku by loging in using this command in terminal:
    ```
    heroku login
    ```
* Add the following variables to the js:
    ```
    var http = require("http");
    var fs = require("fs");
    var path = require("path");
        var mime = require("mime");
    ```
    * The first one gives the key to node.js functionality.
    * The second one is for possibility to interact with the file system.
    * The third is to handle file paths.
    * the fouth is to determine a file's MIME-type.
* Now we need to make a package.json fileand fill it with information like the folling:
    ```
    {
     "name" : "blog",
    "version" : "0.0.1",
    "description" : "My minimalistic blog",
     "dependencies" : {
     "mime" : "~1.2.7"
     }
    }
    ```
* After adding mime plug-in, we need to download it using built-in Node Package Manager by running:
    ```
    npm install
    ```
    and that will create node_modules folder and place all files inside it.
* Create send404() function that will handle the sending of error 404 which appears when requested file doesn't exist; using the following code:
    ```
    function send404(response) {
    response.writeHead(404, {"Content-type" : "text/plain"});
     response.write("Error 404: resource not found");
    response.end();
    }
    ```
* Define sendPage() function that will write a header and then it will send the contents of the file:
    ```
    function sendPage(response, filePath, fileContents) {
    response.writeHead(200, {"Content-type" : mime.lookup(path.basename(filePath))});
    response.end(fileContents);
    }
    ```
* Define how the server handles responses by the following function that will return the content of the requested file or the 404 error otherwise:
    ```
    function serverWorking(response, absPath) {
    fs.exists(absPath, function(exists) {
        if (exists) {
        fs.readFile(absPath, function(err, data) {
         if (err) {
          send404(response)
            } else {
            sendPage(response, absPath, data);
            }
        });
        } else {
        send404(response);
        }
    });
    }
    ```
* Create HTTP server by adding the following code:
    ```
    var server = http.createServer(function(request, response) {
    var filePath = false;

    if (request.url == '/') {
        filePath = "public/index.html";
    } else {
     filePath = "public" + request.url;
    }

     var absPath = "./" + filePath;
    serverWorking(response, absPath);
    });
    ```
* Start server by the following:
    ```
    http.createServer(<some code>).listen(3000)
    ```
* The last one allows us to run the server locally, byt to set a dynamically assigned port number to our app; we need Heroku, so we add the following:
    ```
    var port_number = server.listen(process.env.PORT || 3000);
    ```
* Now add HTML and CSS files.
* After that it's time to hiroku:
    * We need to go to the project folder using terminal.
    * Run 
        ```
        git init
        ```
        it will create empty Git repository in .git/folder.
    * Add and commit as in git.
    * Create Heroku application, that will generate a random name for the application by:
        ```
        heroku create
        ```
    * Push to heroku main by git command.
    * Change the name using:
        ```
        heroku apps:rename customname.
    * Open the app using:
        ```
        heroku open
        ```
    
    


