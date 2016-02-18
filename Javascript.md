#### onload / onready
######standard
```
window.onload = function() {
  // all the things
}
```
######jquery
```
$(document).ready(function() {
// all the things
});
```

#### scope  
use  
`var variableName = {"or whatever other object you wish":"everything in JS is an object"};`  
outside of the scope of a function to ensure a variable is global. Use it inside a function to ensure that scope is limited to that function.
