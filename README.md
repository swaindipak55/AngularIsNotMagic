# Angular Is Not Magic
**AngularJS** is now the most popular and powerful web development framework and backed by Google. AngularJS represent a new paradigm for web application development and it is that much powerful framework that every web develper should know about it. If you are not using it in your project, still you need to understand the concept which will help you to refactor your JavaScript code. Truly I'm saying, it can change your way of thinking. It's better to understand the concept rather than learning APIs. I'm saying my personal experience; when I look at angularJS and trying to understand it, then I understood the real concept of JavaScript. That's why I given the title of this talk as `Angular is not magic`, it is the magic of JavaScript.

In this talk we are going to learn some fundamental JavaScript principles that are necessary to understand hor angularJS works. One of the big problem with angularJS is the `Vocabulary`. Those people who develop this are very smart and they use so many scentific terminology while naming the feature of angularJS. We can say it's just vocabulary or a fancy name to attract or draw the attention of developer. 

Let's get started...

**Magic-1:** 
> Before digging into this, I would like to say that; angularJS use a lot of custom HTML elements and attributes in order to provide any new feature. In angular terminology, these are called as `directives`; don't afread, it's just a name. 

#### Let's understand this from from HTML aside:
  ```
  <html>
    <body>
      <h1>Hi, Good morning</h1>
    </body>
  </html>
  ```
Open this in browser and see the message printed as per the `h1` default font property. Now add an attribute `style="font-size:10px;"` into `<h1>` element as `<h1 style="font-size:10px;">Hi, Good morning</h1>` and run, observe that the DOM has change accordingly. As we can apply an attribute to an HTML element, we can also apply a custom attribute. As per HTML5, we can do this. So I can write this as:
```
<h1 reply="Hello, Very good morning!">Hi, Good morning</h1>
```
Ofcource, it will not change anything in DOM. But We can trace this attribute in javascript, as bellow:
```
<script>
  console.log($('h1').attr('reply'));     // It's jQuery syntax to get the attribute value.
</script>
```
Run this and see the javascript console, it prints :
```
Hello, Very good morning!
```
Even this attribute does not make any change in DOM, but it's exist in DOM. Angular doing the same thing which seems like a magic for us. AngularJS follows a convention that the directive name should be like `ng-reply`.

**Magic-2:** 
> AngularJS solve one of the biggest problem with our javascript application by following some patterns, that is problem with `global namespace`. In many programming languages, `namespacing` is a technique employed to avoid collisions with other objects or variables with same name. 

#### Let's understand this from JavaScript aside:
In a real time project, we have so many JS file created by different developer. There may be a chance that, two developer can create a variable with same name. Then it will be around a day to troubleshoot this in javascript. In java, we have package concept to avoid this situation and we have `block scope` also. 

Note:-  **Scope** refers to where variables and functions are accessible and in what context it is being executed. 

Look at this code:
```
var person = "Deepak";  // This variable is sitting on global namespace, ie; on 'window' object
....
....
// We did some operation by passing the 'person' variable as a parameter to other function
compute(person);
....
....
```
If later on another developer declare same variable for another operation which override the previous variable. For this reason, we need to handle the scope in JS. In javascript, we have only function scope, that means we have to create such pattern using JS function that can avoid this scenario. So we are following a pattern called **Immediately-Invoked Function Expression(IIFE)** coined by **Ben Alman**.
```
function computation() {
  var person = "Deepak";
  // same as above code
}
computation();
```
In this way, we can solve `person` variable collision, but again there may be collision of `computation()` function. Let's modify this:
I can rewrite the above code as : 
```
var computation = function() {
  var person = "Deepak";
  // same as above code
}
computation();
```
But it does not change anything, but I wrote this because your understanding. Again I can modify the above code as bellow:
```
(function() {
  var person = "Deepak";
  // same as above code
})();
```
Instead of creating a variable to hold the function reference and call it explicitely, we can create a anonymous function and call immediately. This solves our problem.

AngularJS does the same thing using constructor and provide an object called `$scope` to each constructor to hold the data that are relevant to this constructor. It follows only a design patterns to resolve the naming collision. 
```
angular.module("myApp")
       .constructor("MyConstructor", function($scope) {
          // constructor logic goes here
       });
```
We are passing the constructor function defination only, angular callback it internally.

**Magic-3:**
> In most of the angular training, you have seen this example in angularJS:

In HTML:
```
<div ng-app="myApp" ng-controller="MyCtrl">
  <span>Enter some text : </span>
  <input type="text" ng-model="text">
  <div>
    <h3>Hello, you are entering: {{text}}</h3>
  </div>
</div>
```
In AngularJS:
```
angular.module("myApp", [])
			 .controller("MyCtrl", function($scope) {
});
```
Right click [here](https://jsfiddle.net/swaindipak55/yovoewwL/) and open in a new tab.

Here is some pure JS code which do the exactly same magic :

In HTML:
```
<div>
  <span>Enter some text : </span>
  <input type="text" id="text">
  <div>
    <h3>Hello, you are entering: <span id="result"></span></h3>
  </div>
</div>
```

In JS:
```
var text = document.getElementById("text");
text.addEventListener("input", function() {
	document.getElementById("result").innerHTML = text.value;
});
```
You can check the output [here](https://jsfiddle.net/swaindipak55/t87pdjvk/)

**Magic-4:**
> **Dependency Injection** is one of the best feature provided by angularJS. Have you ever think about this? How this feature given by angularJS?
`Dependency Injection` is one way to connect an object to another. We have another two way to connect an object in Java.
- Dependency Create
- Dependency Pull
Dependency Injection bit popular than other two ways, because of the following reason:
*If we know that a target object has to be instantiated in our context to proceed further then, why to wait to create or pull, when it is required? why not create it in loading or deployement time and inject it whenever needed.*

From angular point of view, dependency injection is, instead of creating an object inside a function; pass the function defination as an argument to the function.
For an Example;
```
function Person(name) {
  this.name = name;
  // do other operation
}
function doSomeThing() {
   var deepak = new Person("Deepak");
   // do some operation on this 'deepak' object
}
```
Instead of doing this, we can pass the 'deepak' instance to the 'doSomeThing()' function which makes it loosly coupled. So we will create the person object where the 'doSomeThing()' function called and pass that to 'doSomeThing()' function.
```
function doSomeThing(person) {
   // do some operation on 'person'
}
var deepak = new Person("Deepak");
// call the function by passing 'deepak' reference to it
doSomeThing(deepak);
```
or 
```
doSomeThing(function(name) {
  this.name = name;
  // direct define the constructor function here
});
```
Angular doing this things, but here the chalenge is how angular identifies the all the arguments and inject accrodingly. Let's see this example:


**Magic-5:**
> **Routing** 

**Magic-6:**
> **Singleton Object**, Angular provides singleton mechanisim by using `provider`, `factory` and `service`. All these are creating singleton object for our application. This pattern is not interduced by angularJS. We can also create singleton object in pure javascript. Angular create the singleton objects in same fashion.

Before moving towards singleton pattern, let's understand understand something about javascript constructors:
```
function Person(name) {
   this.name = name;
}
var deepak = new Person("Deepak");
```
Note- Here `new` is essential, otherwise the keyword `this` inside the `Person` constructor will be equal to `Window` instead of `deepak`.

**What happens when a constructor is called?**
When `new Persson()` is called, Javascript does the following four things:
- 1. It creates a `new` object.
- 2. It sets the `constructor` property of the object to `Person`.
- 3. It sets up the object to delegate to `Person.prototype`.
- 4. It calls `Person()` in the context of the new object.

Here my intenstion is to make you understand about 3rd point, that is `constructor` property.
This means, the following things must be true:
```
deepak.constructor == Person  // true
deepak instanceof Person      // true
```
If you assign `constructor` property to any other object:
```
var Employee = new function() {
    this.name = "Hello";
}
deepak.constructor = Employee;

deepak.constructor == Employee // true
deepak.constructor == Person   // false
deepak instanceof Person       // true
```
I can't elaborate more about `constructor` property as it is beyond the scope of this talk.

Let's create a single object in javascript:
```
var SingletonFactory = (function(){
    function Person(name) {
        // This is just a private constructor, If you have any initialization; do it here
        this.name = name;
        
        this.print = function() {
            print(this.name);
        }
    }
    var instance;
    return {
        getInstance : function() {
            if (instance == null) {
                instance = new Person("Deepak");
                instance.constructor = null; // Hide the constructor function from outside. 
		//Comment/Uncomment this line and observe the result 
            }
            return instance;
        }
   };
})();

var s1 = SingletonFactory.getInstance();
var s2 =  SingletonFactory.getInstance();
if (s1 == s2) {
    print("Both are singleton");
}
s1.print()
s2.print();
print(s1.constructor);
```
You can run this example [here](http://rextester.com/TNRV42283)
