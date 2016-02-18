###### `__misc__`
dev / prod base url
```
$host = ((strpos($_SERVER['HTTP_HOST'], "__value_of_interest__")) !== false ) ? $_SERVER['HTTP_HOST'] : "" ;
```
show errors
```
error_reporting(E_ALL);  
ini_set("display_errors","on");  
```
ternary
```
$result = (a == b) ? 'equal' : 'not equal';
```
### arrays
Query for value  
```
$key = array_search($__string__, $__array__)
``` 
returns **FALSE** if no key is found
returns first instance only
### wordpress
Page ID  
```
get_the_ID()
```