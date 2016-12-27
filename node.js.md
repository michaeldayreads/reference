# debug hacks

`console.log(__filename);` is a simple way to trace where you are when exploring a new code base.

# Commands
pass  

# Other

## ES6

### Arrow functions

Server example:

```
var http = require('http');

http.createServer(function(request, response) {
  response.writeHead(200);
  response.write('Ahoy Matey!');
  response.end();
}).listen(80);
```

_becomes_

```
var http = require('http');

http.createServer( (request, response) => {
  response.writeHead(200);
  response.write('Ahoy Matey!');
  response.end();
}).listen(80);
```


# sources

[Learning Node, 2nd Edition](https://www.safaribooksonline.com/library/view/learning-node-2nd/9781491943113)
[Node Beginner](http://nodebeginner.org/)