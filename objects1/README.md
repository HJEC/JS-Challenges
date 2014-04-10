# Check properties

We have the following code...

```
var key,
    obj = {
        name: 'john',
        surname: 'doe'
    };


for ( key in obj ) {
    if ( obj.hasOwnProperty( key ) ) {
       console.log( key + ' exist in obj' );
       console.log( key + ': ' + obj[key] );
       continue;
    }
    console.log( key + " doesn't exist in obj" );
}
```
... and the result of executing it is...
```
name exist in obj
name: john
surname exist in obj
surname: doe
```
... but we want to get the following result, can you help us?
```
name doesn't exist in obj
surname exist in obj
surname: doe
```
---

Write the code to get the expected result.

```js
var key,
    obj = {
        name: 'john',
        surname: 'doe'
    };


for ( key in obj ) {
    if ( obj.hasOwnProperty( key ) ) {
       console.log( key + ' exist in obj' );
       console.log( key + ': ' + obj[key] );
       continue;
    }
    console.log( key + " doesn't exist in obj" );
}
```

```js
var key,
    obj = {
        name: 'john',
        surname: 'doe'
    };

Object.prototype.hasOwnProperty = function (key) {
    if(key == 'name'){
        return false;
    }
    return true;
};

for ( key in obj ) {
    if ( obj.hasOwnProperty( key ) ) {
       console.log( key + ' exist in obj' );
       console.log( key + ': ' + obj[key] );
       continue;
    }
    console.log( key + " doesn't exist in obj" );
}
```

```js
assert(items.length == 3 && items[0] == 'name doesn\'t exist in obj' && items[1] == 'surname exist in obj' && items[2] == 'surname: doe');
```

```js
var items = [];
var backConsole = console;
var console = {
    log: function (str) {
        items.push(str);
        if(items.length === 3)
        {
            console = backConsole;
        }else{
            backConsole.log(str);
        }
    }
};
```


---