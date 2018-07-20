# ES6 - New Stuff

A short description of new features in ECMAScript 6. This evolved out my notes as I was writing some UI code and found I needed a fast refresher on what was in ES6 and how it had changed from ES5.

Disclaimer, this has not been wordsmithed, reviewed for accuracy, or edited in anyway -- I don't promise it's 100% accurate. It's just one guy's notes taken while furiously reading about ES6.

## String Interpolation

About time.

``` javascript
let first = 'Wilma';
let last = 'Flintstone';
let name = '${first} ${last}'
```

## Let, Const, and our old friend Var

In short, `var` works as before; `let` is similar to `var` but with a scope restricted to the enclosing block; and, `const` will cause errors if the value referenced is redefined. Note that if a `const` is initialized to an object, like an array, the binding to the object is const, but not the content of the object.

``` javascript

// Note, there are many more examples than shown here -- it would be a
// great exersicse to actually code this up in something and run it on,
// say, node - perhaps even driven by a test. Oh well, no time for that
// that right now. In the meantime, this example gives a sense of how
// the new features work.

let a = 1;
let b = 2;
const c = 3;
const ar = [ 42, 43, 44 ];

if (true) {                // Creating a block for this example.
  let d = 4;
  var e = 5;
  foo(a + b + c + d + e);  // Legal
  baz(ar) ;                // Legal
  c = 100;                 // Error, c is const.
  ar[3] = 200;             // Legal.
  ar = [ 'xyzzy' ] ;       // Error, ar is const.
}

foo(a);  // Error: outside of scope.
foo(e);  // Legal, e is "var" and is visible out side defining scope.
```

## New Closure Syntax

This example of the new syntax uses a variable binding, to name the closure. The `=>` operator is used to introduce the body (sort of like a lambda, kinda). ES6 now supports optional parameters, and a `...` operator in the parameter list, similar to Ruby's splat, `*`, operator.

``` javascript
var someMath = (a, b = 1) => {     // The new syntax. If not supplied, b
}                                  // defaults to 1.

var newMethod = (...vals) => {     // When in a formal parameter list, ...
                                   // means "condense all the parameters
}                                  // into an array named vals."

newMethods(1, 2, 3);               // For example, inside the function body
                                   // of newMethod, vals is [1, 2, 3].
                    
let ar = [9, 8, 7];                // When ... appears in the call, the
foo(...ar);                        // array is expanded into a list of 3
                                   // parameters, exacly the same as if
                                   // this were written as foo(9, 8, 7).
```

Another nice thing is that within a block, a function defined is only visible within the scope of that block.

``` javascript
 {
   function flimflam () { return 1; }     // Outer scope definion.
   flimflam();                            // -> 1, as expected.  
   {
     function flimflam () { return 2; }   // Redef, only inner scope.
     flimflam();                          // -> 2, calls more local one.
   }
   flimflam();                            // -> 1, back to outer scope.
 }

```

## Sets, The `for`-`of` Loop, and Maps

Sets are ordered collections of unique values. For-of loops are just a new syntax, much like the for-in loop. Maps are key-value storage objects where key and value can be any object kind of value. Keys are unique.

``` javascript
let hand = new Set();

hand.add('AS')
hand.add('KS')
hand.add('QS')
hand.add('JS')
hand.add('TS')
hand.add('QS')   // Adding second Queen of Spades, no effect.

for (let card of hand) {
  // Each time through this loop, card will be set to 'AS', 'KS',  
  // 'QS', etc.
}

var employers = new Map();

employers.set('George', 'Cogswell Cogs');
employers.set('Fred',   'Bedrock Stone & Gravel');
employers.set('George', 'Spacely Sprokets');  // Redefines this map entry.

employers.size;    // -> 2, There's only 1 George and 1 Fred.
employers.keys();  // -> Iterator for each key in the map.

for (let [k, v] of employers) {
  k;  // -> In turn, 'Fred', then 'George'.
  v;  // -> In turn, 'Bedrock...', then 'Spacely...'.
}
```

## Classes: Statics (Class Methods) Getters, & Setters

Instead of standing on your head to define a class, the `class` keyword works like it does in many other languages. Although, not shown in this example, the `extends` keyword allows subclassing, as in `class Person extends Animal { }`. Use `super` to access the base superclass's members.

Class-level methods are defined as a `static` class method and do not need an object instantiation to be called. Getter and setter methods are about what one would expect. 

``` javascript
class ObjectWithName {
  static Version() {                  // Simple method syntax.
    return "ObjectWithName v2.3.1";
  }
  constructor(initialName) {
    this.name = initialName;
  }
  get Name() {
    return this.name
  }
  set Name(newName) {
    this.name = newName;
  }
}

// Static methods are, essentially, class methods and are simply called
// on the class name...
some_report_method(ObjectWithName.Version());

// Using getters & setters...
let framitz = new ObjectWithName("Rose");
framitz.Name = "Lily";
some_method(framitz.Name);   // Passes "Lily".
```
