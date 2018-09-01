---
layout: post
title: Dart 05 | Object-Oriented
subtitle: In this article ,we will talk about class,interface and object.
tags: [dart]
---
# Class
Dart is object-oriented programming. So it must have the concept of class. We have the class then we have the object. Let us go to our learning travel with me.

# How to define a class
The keyword `class` is necessary to our defining. Example is beneath.
```dart
class Example {
  Example() {
    print("It is an example.");
  }

  var name = "niebin";
  dynamic age = 29;

  void printMessage() {
    print("I am nie bin from china,A positive man.");
  }
}


```        
The definition above is similar to the Java, the constructor as well. The syntax of definition class is as this :
```dart
class class_name{
  [fields]
  [getters/setters]
  [constructors]
  [functions]
}

```
As you can see, It is straightforward.But you should remember that there are not identifiers before the `class.`This is very different from the Java.

# How to use
Once we define a `class` in the file, then we can use it. There are two ways for instancing the `class`. The one have the keyword `new` , then another one has not. Examples:
```dart
void main() {
  var ex = Example();
  var ex2 = new Example();
  ex.name = "s";
  print(ex.name);
  ex2.age = 18;
  print("my is age is ${ex2.age}");
  ex.printMessage();
}
//will print
/**
It is an example.
It is an example.
s
I am age is 18
I am nie bin from China, A confident man.
*/
```
In the example above, we can see the ways for calling functions and fields.  Just use the symbol dot `.`.This kind of way is prevalent in other programming languages.

# Constructors
When you define a constructor in the dart language, You can define it as a common function but don't have the return type. If you want to override it, you can not use it as the same the but use the named constructor as the beneath.
```dart
void main() {
  var ex = Example.constructor1(1);
  ex.printMessage();
}

class Example {
  Example() {
    print("It is an example.");
  }

  Example.constructor1(int a) {
    print("a is $a");
  }


  void printMessage() {
    print("I am nie bin from china,A positive man.");
  }
}

```
There are two constructors in the example, The first normal constructor with the same name of Example class, the second one is the named constructors. The syntax is a sample, and we need use the `class name` first, then set constructor name with it. The `constructor1` above is the constructor name.

# Inheritance
Like many other languages, we support the inheritance.The keyword is `extends`,the syntax is `class child_class_name extends parent_class_name`.If you want to override the function in the parent class, make the function is the same as the parent's, you will override it. The example is beneath.
```dart
class Example {
  Example() {
    print("It is an example.");
  }

  Example.constructor1(int a) {
    print("a is $a");
  }

  void printMessage() {
    print("I am nie bin from china,A positive man.");
  }
}

class ChildExample extends Example {
  @override
  void printMessage() {
    print("this is override funtion of print message.");
  }
}

```   
# The keyword
In the class, there are some relevant keywords.
- `this`   
this keyword is the object instance of the current class.It can call its field and functions.
- `super`  
If you override a function,it can have a `super` keyword,that you can call the function or field of the parent class.
- `static`   
A static field or function is referenced with the class, and you do not need to instance them and call them directly.

```dart
void main() {
  print("this age is ${Example.age}");
}

class Example {
  Example() {
    print("It is an example.");
  }

  static var age = 1;
}

```
# Interface
If you inheritance a class,but you do not want their function body and what a clean function, then the interface is coming.   
### How to define a interface?
This kind of interface definition is so different  with other programming. It do not use the keyword `interface`,but use the keyword `class`,which is used to define the class,I am astonished by it by the way.But you should be care about that if you have implement a interface,**you should override every function** in the parent class.
```dart

class Example {
  void printMessage() {}
}

class ChildExample implements Example {
  @override
  void printMessage() {
  }
}
```
Above this example,we can just understand that a interface is a class,but if you use `implement` keyword to implement a class ,it become a interface that you must override its every function.
### How to use an interface  
 Don't like the Java language,we can implement a interface with its fields and functions.that is cool to override it. The example as below.
```dart

class Example {
  Example(c) {
    print(c);
  }

  void printMessage() {}
  var a = 0;
  static var b = 1;
}

class ChildExample implements Example {
  @override
  void printMessage() {}

  var a = 1;
  @override
  var b = 2;
}
```
You need know ,we can not override a `static` field of a interface and dart also support the multi implement.

# Cascade operator(..)
If you use a object in the same time but call it for some many times, there is a symbol `..` to help you use the object convenience.Examples are below.
If we have the this definition:
```dart
class Example {

  void printMessage() {}
}
```
Normal using:
```
var c = ChildExample();
c.printMessage();
c.printMessage();

```
With `..` symbol
```dart
var c = ChildExample();
c..printMessage()..printMessage();
```
This can save you coding time and beautify your code.

# Summary
Today, we learn about the object-oriented elements in the dart, such as class, interface and object. It is very similar to other object-oriented languages but has its properties. If you have traveled with the other article about dart before, you could code in a real project now, for the inside basic knowledge about the dart is going through with these articles. If you want to travel further, just following with me, we have a nice trip.

Thanks.
