---
layout: post
title: Dart 04 | Function
subtitle: Let's look at the function.
tags: [dart]
---
# Function
In a developing programming,if you want to unit some code together,first thing we thinking about is the function.It was created by computer professors at the beginning of a programming.
So let us look at that how to define it or use it.
# How to define
the style like this:

```dart
//the return type is not necessary too ,if not should be void
[return type] function_name(){
  //statements:this is function body that you can do some thing here.
  [return value] //this is not necessary  
}

```
real example as below.
```dart
int plus10(int a) {
    print("call plus ten.");
    return a + 10;
  }

```
The example above define a function named plus10,return int type and return the input plus with 10.It is easy understand and write ,If you similar with java,it is same as the function of java but do not have the identifies ,such as public.As the java ,there is only one return value in the function of dart.The parameters are defined with the style of `type variable_name`.Also like java.

# How to use?
When we define a function ,we need to use it. Here are example:
```dart
var b =plus10(1);
```
Above, we just need to use the name of a function and a brackets, if there are some parameters,you would pass the values of the corresponding parameters within the brackets.then the call will done.


The defining and using of a function are easy,but you should have to know some special feature in it.
# Inside function   
First is the defining a function inside a function. This is different with java or other old language. Example is in beneath.

```dart
void printHello() {
  int plus10(int a) {// this is nesting function in a function. but it only use in the function.
    print("call plus ten.");
    return a + 10;
  }

  var b = plus10(1);
  print("b = $b");
}
```
# Optional positional parameters
In the dart, if there is not an override function with the same name,which means if you can not define a function with one name at the same scope. But dart support the optional positional parameters and you can use it to achieve your purpose.Example is following,The symbol is `[]`
```dart
void main() {
  printHello();
  printHello(1);
}

void printHello([var a]) {
  print("a = $a");
  print("no a");
}

```
What is the optional parameters,which mean you can use them if you like,but not the necessary to use them.This is very similar with override function in java. But there are some different about it. Its calling is same,but its body is very different. In java they are complete function body,but in dart you need check with youself.
The syntax of the positional parameters is `type function_name(type1 v1,[type2 v2])`,The structure is not necessary and the number of the parameters is varied,which means you can put nothing or every [] parameters here.

# optional name parameters
The symbol is `{}`,The name parameters is defined in the `{}`.Example below.
```dart
void main() {
  printHello();
  printHello(a: "1");
}

void printHello({a}) {
  print("a = $a");
  print("no a");
}

```
We just need to define variables in the symbol `{}`, when you use it ,then you use the symbol `:` as `a:1` that assign the value of 1 to the variable of `a`.This are very similar with the default value in `kotlin`.But you should be careful about use the optional positional parameters by assigning value of style.
```dart
void main() {
  printHello();
  printHello(a = 2);//this is not assigning the 2 to the second variable `a` of `printHello` but the first. This may be not within your expecting.
}

void printHello([b, a]) {
  print("a = $a");
  print("a = $b");
  print("no a");
}

```

# Optional default parameters
This kind of parameters is an expansion of  the name parameters.If you don't put parameters to the default parameters,the system with use the default one.Example is beneath.
```dart
void main() {
  printHello();
  printHello(a: 2);
}

void printHello({a = 1}) {
  print("a = $a");
  print("no a");
}

```
the using is the same as the name parameters,only have the default value.

# Lambda Functions
Lambda function is very fashion in the modern language.Because the using is very sample and convenience, so many people are like it.The syntax is as this `[return type] function_name(parameter_variables) => expression `,There is a example.
```dart
void main() {
  printHello();
}

void printHello() {
  print(getTen()); // print 10.
  print(plusTen(1)); //print 11.
}

int getTen() => 10;

int plusTen(a) => a + 10;

```
As you can see, the lambda function is used in some logical with sample.
In some modern language, a function always support the function as a variable.Example like this:
```dart
void main() {
  print(plusNine(3));
}

var plusNine = (a) => a + 9;

```
There are many things about functions, but I will talk about it in the next few article to make sure we know the base concept at first.  

# Typedef
The keyword `typedef`,which is used in calling a function by defining a variable,the function is the same with the same parameter types and the same numbers of the parameter. That means if the types, numbers,and the orders of the parameters are the same,you can assign to the same typedef variables.Examples are below:
```dart
typedef callFun();
typedef twoOper(int a, int b);

void main() {
  callFun call = printHello;
  call();
  call = printWorld;
  call();
  int a = 9, b = 10;
  twoOper two = add;
  print("add = ${two(a, b)}");
  two = min;
  print("min = ${two(a, b)}");
}

void printHello() {
  print("hello");
}

void printWorld() {
  print("world");
}

int add(int a, int b) {
  return a + b;
}

int min(int a, int b) {
  if (a > b)
    return b;
  else
    return a;
}
```
Will print:
```
hello
world
add = 19
min = 9
```
This is very convenience to use a function as variable with the keyword `typedef`.
Good luck!

The End.
