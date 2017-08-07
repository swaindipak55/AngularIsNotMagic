# Angular Is Not Magic
**AngularJS** is now the most popular and powerful web development framework and backed by Google. AngularJS represent a new paradigm for web application development and it is that much powerful framework that every web develper should know about it. If you are not using in your project, still you need to understand the concept which will help you to refactor your JavaScript code in your project. Truly I'm saying, it can change your way of thinking. It's better to understand the concept rather than learning APIs. I'm saying my personal experience; when I look at angularJS and trying to understand it, then I understood the real concept of JavaScript. That's why I given the title of this talk as `Angular is not magic`, it is the magic of JavaScript.

In this talk we are going to learn some fundamental JavaScript principles that are necessary to understand hor angularJS works. One of the big problem with angularJS is the `Vocabulary`. Those people who develop this are very smart and they use so many scentific terminology while naming the feature of angularJS. We can say it's just vocabulary or a fancy name to attract or draw the attention of developer. 

Let's get started...
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

> AngularJS solve one of the biggest problem with our javascript application by following some patterns, that is problem with `global namespace`. 

#### Let's understand this from JavaScript aside:

