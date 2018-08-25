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
