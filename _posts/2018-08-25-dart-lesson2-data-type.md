---
layout: post
title: Data types
subtitle: We will talk about the data types of the dart language.
tags: [dart,flutter]
---
# Support Data Types
There are five types in dart:
- numbers
- Strings
- Booleans
- Lists
- Maps
Before we talk about data types,we would see how to define the variable in dart.To define a variable ,there are many ways to do it.The keywords are `var` and `dynamic`

```dart
String nickName ="Nie Bin" ;//define a variable named nickName and the type is String
var age = 18 ; // define a variable named age and the type is dynamic with int ,if you assign the age ="nie bin" ;,there will be an error.
dynamic address = "ShangHai";  // the variable name is address and have a dynamic type that you can assign any to it, if you assign address =1 ; there will not be an error.

```
The code above is about how define a variable that can assign a value again, you want to define a constant that do not change in the compile time, you should use the keywords of `const` and `final`

```dart
const NIE_BIN = "Nie Bin"; //as you see   the value is 'Nie Bin',but you can not assign again.
final AGE = 18; // you can only set once,if you assign again it will say error.
```
If you define a variable that is not `final` or `const`, but not assign its value ,it will assign a value of `null`, whatever its type is.   

# Numbers
There are only two types numbers in dart,which are `int` and `double`. The `int` represents the integers and the `double` represents fractional numbers. So it is very ease to use and remember.example below :

```dart
var a = 1 ; //auto convert to int.
var f = 1.1 ; //dynamic type to double.
print(a);
print(f);
```
As you know, the dart is an object-oriented language,so the variables of `a`,`f` are common object. These have some properties and  functions. such as `isEven` , `sign` and so on. `int` is a class that extends `num` class.if you want to know more about its properties or functions , you can look at the source in an IDE.The other data types if you want to know are same as this way.

# Strings
`String` is very common in developing,there are two ways to represent a single line of a `String`. The one is single quotes and the another one is double quotes. If you want to use the multi line of a `String` use the triple quotes.

```dart
var single_quote = 'this is single quote that is used to represent a single line string.' ;
var double_quote = "this is double quote that describe a single line string as well." ;
var triple_quote = """
  this is a triple quotes that are used to describe a multi lines strings. it is very similar to the python.
""" ;
```
We have a basic way of using string, let's go far more deep with its operator of `concatenation` and `interpolation`.
`concatenation` is just plus a string to another one with sign of `+`.
`interpolation` makes the string as a variable in the quotes ,just use the characters `$` or `${}`.
Examples are in the following:

```dart
  var single_quote = 'single quote';
  var double_quote = "double quote";
  var triple_quote = """triple quote""";

  var concatenation = 'this ' + single_quote;
  var inter1 = 'that ' + 'is interpolation example1:$double_quote';
  var inter2 = 'that ' + 'is interpolation example2:${triple_quote}';
  print(concatenation);
  print(inter1);
  print(inter2);

```
`String` is a class that  implements `Comparable<String>` and `Pattern` and have some properties,functions two.if you want to know more about them ,just look its source code.


# Booleans
The keyword is `bool`.its values have just two options of `true` and `false`. If a type is not a boolean and you use as a boolean ,it will compare with true value,the all of them are false,because the others are not equal `true`. Basic Example:

```dart
var isCat = false;
 bool isT = true;
 print(isCat);
 print(isT);
```
# List
List is an array in dart and have is order that start with zero and end in n-1,the n is its length.the list is same as the language of java.
