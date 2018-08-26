---
layout: post
title: Dart 03 |Operators
subtitle: There are some operators and sentences in this article.
tags: [dart,flutter]
---
# Operators
There are six operators in dart:  
1. arithmetic
- relational
- check type
- bitwise
- assignment
- logical
- conditional

#### 1. Arithmetic
The arithmetic operators are the same as the java, but the `~/` is an exception in dart.

| 1 | 2 | 3 |
|------|------|------|
| `+` | `-` |  `*` |
|  `/` | `~/` divide but return integer | `-expr` reverse the sign |
| `%` | `++`  | `--` |   

```dart
 var a = 3 ~/ 2;
 print(a); //print 1
 a = -a;
 print(a); //print -1
```

#### 2. relational   
Same as the java.

| 1 | 2 | 3 |  
|------|------|------|
| `>` | `<`| `>=`|
|`<=` | `==`| `!=` |

```dart
 var a = 1;
 var b = 2;
 var isLarge = a > b;
 var isLow = a < b;
 print(isLarge); //print false means that a is not larger than b.
 print(isLow); // print true means that a is lower than b.
```
#### 3. check type

|1|2|
|--|--|
|`is`|`is!`|
|check the variable is or not the appoint type| the reverse ,check `is not`|

```dart
 var a = 1;
 var isInt = a is int;
 var isDouble = a is! double;
 print(isInt); //print true.
 print(isDouble); //print true.
```
#### 4. bitwise
All the bitwise operators are operating with its responsive place.

| operator | description | example |
|----|----|----|
|`&`AND | a & b | if its responsive bits are same as `1` then take the one,otherwise zero.|
| OR | the sign is a Vertical line| if have an one ,take one |
| `^` XOR | a^b |if different take one ,otherwise take zero|
| `~` NOT| ~a |this one is very special , the `~1 == -2` just invert the a|
| `<<` left shift | a<<b| the bits of a shift left b step.|
| `>>` right shift | a >> b | the bits of a shift right b step|

If you understand the the `~` operator very different , if can look at these [Answers](https://stackoverflow.com/questions/791328/how-does-the-bitwise-complement-operator-tilde-work) and [Complement](https://www.programiz.com/java-programming/bitwise-operators#complement).

#### 5. assignment
There some common operators about assignment operator, such as `+=`.

| operator | explanation |
|---|---|
| `=`| var a = 12; //just a sample assign|
| `??=`|if variable is null then assign it|
| `+=` | a +=1 means a =a+1,the other multi assignment is the same use |
| `-=`,`*=`,`/=`| the using is the same as the `+=` but have the different operators|

#### 6. Logical
there are three operators in logical operators.

|operator| explanation|
|---|---|
|`&&`| both true will return true.|
|`OR`| if have true return true.|
|`!` | invert variable ,if true return false |

#### 7. Conditional

This is same as the `?:` expression in java. The mean is that if true return a else return b.

```dart
 var a = !true;
 var content = a ? "this is true" : "this is false.";
 print(content); //will print 'this is false.'
```

The End.