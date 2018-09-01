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
The End.
