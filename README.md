# Primus.IO

[![Build Status](https://travis-ci.org/cayasso/primus.io.png?branch=master)](https://travis-ci.org/cayasso/primus.io)
[![NPM version](https://badge.fury.io/js/primus.io.png)](http://badge.fury.io/js/primus.io)

Primus.IO makes working with [Primus](https://github.com/3rd-Eden/primus) a little slicker.

## Instalation

```
npm install primus.io
```

## Usage

### On the Server

```
var Primus = require('primus.io');
var server = require('http').createServer();

var primus = new Primus(server, { transformer: 'websockets', parser: 'JSON' });

primus.on('connection', function (spark) {

  // listen to hi events
  spark.on('hi', function (msg) {
    
    console.log(msg); //-> hello world

    // send back the hello to client
    spark.emit('hello', 'hello from the server');

  });

});

server.listen(8080);
```

### On the Client

```
var primus = Primus.connect('ws://localhost:8080');

primus.on('open', function () {

  // Send request to join the news room
  primus.emit('hi', 'hello world');

  // listen to hello events
  primus.on('hello', function (msg) {

    console.log(msg); //-> hello from the server

  });

});

```

Check the examples for more use cases.

## Features

- Emit-style `emit()` w/ arguments
- Client & server side "ack" callbacks
- Rooms
- Serves `/primus.io.js`

## Todo

- Finish to add tests.
- Add broadcast to all connected clients
- Add more documentation

## Run tests

```
make test
```

## License

(The MIT License)

Copyright (c) 2013 Jonathan Brumley &lt;cayasso@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.