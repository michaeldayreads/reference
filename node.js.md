# debug hacks

`console.log(__filename);` is a simple way to trace where you are when exploring a new code base.  

Drill into an object

```javascript
const foo = require('util');
console.log(foo.inspect((object, false, null)):
```

# Commands
pass  

# modules

Exporting a single function for use in another file...  
```javascript
// attempting to find the difference between exports and module.exports
// https://stackoverflow.com/questions/7137397/module-exports-vs-exports-in-node-js#7142924

borked = (name) => {
  return{
    deeper: () => console.log(`it is borked ${name}!`)
  };
}

works = (name) => {
  return {
    deeper: () => console.log(`Looks like it works ${name}!`)
  };
}

exports.borked = borked; // actually works, attempting to break ...
// per above, exports is a global, so can be overwritten by other exports?
module.exports.works = works; // module is a local
```


# Other

## ES6

### Arrow functions

Server example:

```javascript
var http = require('http');

http.createServer(function(request, response) {
  response.writeHead(200);
  response.write('Ahoy Matey!');
  response.end();
}).listen(80);
```

_becomes_

```javascript
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

[Node docs](https://nodejs.org/api/)