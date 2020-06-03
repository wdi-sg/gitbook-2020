# Fixing Scope Errors

### Basic block scope

Javascript looks out, but not in.

```text
var message = "Hello";

function doSomething(){
  console.log( message );
}

doSomething();
```

`message` is defined "globally" and can be seen everywhere.

```text
function doSomething(){
  var message = "Hello";
}

console.log( message );
```

Variables defined inside of functions can only be seen inside the function and from any functions called inside the function.

### Still basic block scope + async timing

People commonly make this error:

```text
for (var i=0; i<5; i++) {

  var link = document.createElement("a");

  link.innerHTML = "Link " + i;

  link.addEventListener('click', function() {
    console.log(i);
  });

  document.body.appendChild(link);
}
```

The value of `i` is not held inside the event listener function.

## solutions

### Use foreach

```text
var links = [];

for (var i=0; i<5; i++) {

  links.push( document.createElement("a") );

}

links.forEach(function(link, i){

  link.innerHTML = "Link " + i;

  link.addEventListener('click', function () {
    console.log(i);
  });

  document.body.appendChild(link);
});
```

### Local function scope

```text
var setLink = function(i){

  var link = document.createElement("a");

  link.innerHTML = "Link " + i;

  link.addEventListener('click', function () {
    console.log(i);
  });

  document.body.appendChild(link);
};

for (var i=0; i<5; i++) {
  setLink(i);
}
```

### Closure Scope 2:

Immediately Invoking Function Expression

```text
for (var i=0; i<5; i++) {

  (function(i){

    var link = document.createElement("a");

    link.innerHTML = "Link " + i;

    link.addEventListener('click', function () {
      console.log(i);
    });

    document.body.appendChild(link);
  })(i);
}
```

Pass the parameter you want to "hold onto" into the `function expression`

## Pairing Exercise

* After each line write a console.log\("what is happening at this line", variable-to-console.log \)
* Callbacks and scope become more clear when you understand the values of each thing at each place in the program.
* Try each example out.

