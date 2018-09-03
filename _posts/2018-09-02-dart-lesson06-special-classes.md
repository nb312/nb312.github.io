---
layout: post
title: Dart 06 | Special Classes
subtitle: Some special types class in dart!.
tags: [dart]
---
# Runes
String is coded by UTF-16 in dart, if you want know the integer code an Unicode,then you need to know Runes.

### What are the Runes
Runes are  the integer representing the Unicode code point.For example,if the string is `Hello`,so we can get its Unicode.
```dart
String hello = 'Hello';
print(hello.codeUnits);//[72, 101, 108, 108, 111]

```
Then we look at the runes as below.
```dart
  print(x.runes); //(72, 101, 108, 108, 111)

```
### How to use
As we can see,the result is almost same as the `codeUnits` above.Why is the dart having a same feature with different name.Let's go to continue our travel with Runes.When I look the source code inside  the class`Runes`,it is said that `Runes` extend the Iterable<int>, which is the same as the List.   
If you want convert a Unicode to a string ,just like this.
```dart
var r = Runes("\u{0048}\u{0065}\u{006C}\u{006C}\u{006F}"); // make sure it is an UTF-16 Unicode.
 var str = "";
 r.forEach((int rune) {
   str += String.fromCharCode(rune);
 });

 print(str);
```

# Enumeration
The enumeration is similar with class.It is used in the places that need manage some similar places.Here are example.
```dart
void main() {
  var v = Video.START;
  print(v.index); // print 0.
  v = Video.PLAYING;
  print(v.index);// print 1.
}

enum Video { START, PLAYING, PAUSE, STOP }

```
# Collect
Collect is useful data structure,which can manage your data very well.There are several types of collect,such as Set,HashMap,LinkedList,Queue.Examples:
```dart
import 'dart:core';
import 'dart:collection';

void main() {
  var a = Set();
  for (var i = 0; i < 10; i++) {
    a.add(i);
  }
  for (var i = 0; i < 3; i++) {
    print("------------------");
    print(a);
  }
  HashMap<String, String> hashMap = HashMap();
  hashMap["a"] = "a";
  hashMap["b"] = "b";
  print(hashMap);

  Queue q = Queue();
  for (var i = 0; i < 10; i++) {
    q.add(i);
  }
  while (q.isNotEmpty) {
    var element = q.removeFirst();
    print(element);
  }
}
```
The basic using is either same as list or the map.So it is easy.

# Generics
As  the example say above,a collection have different types,it is legal in dart.If you want to use the same type,you need the `Generics`,we take the List as an example.
```dart
var strList = List<String>();
 strList.add("Hello");
 strList.add("world");
 strList.add("!");
 for (var str in strList) {
   print(str);
 }
```
If you  want use the Int type ,it is easy to change.Just like this `var intList=List<int>()`,the using of it is same as the type of `String`,but the type must be int.Be careful about the type `int`,which is a class that not same as the Java.The other collections have their `Generics` yet,which is similar to List.

### How to define with a generics
In function,like this:
```dart
void printT<T>(T t) {
  print(t);
}
```
In class,like below:
```dart
class Student<T> {
  void printMessage(T t) {
    print(t);
  }
}
```
Then use them as beneath:
```dart
void main() {
  printT("hello");
  var stu = Student<String>();
  stu.printMessage("world!");
}
```
It is very easy to define or use the generics,but the feature and application are wide.

# Exception
When our application or program are in the runtime,sometimes,we get an error within it.At this situation,we usually need to handle the exception.The class `Exception` is representing a exception and all exceptions that are throw in dart is implementing the class `Exception`.

### How to handle an exception
When an exception occurs,we use the `try`  handle it. The Example:
```dart
void main() {
  dynamic s = "";
  try {
    int.parse(s);
  } on FormatException {
    print("format exception");
  } catch (e) {
    print(e);
  } finally {
    print("Game over!");
  }
}

```
It is same as the Java.
### Throw
If you want to throw an exception,Example beneath:
```dart
if(a!=0){
  throw Exception("This is exception that a is not equal zero.");
}

```

### Custom Exception
If you want to custom an exception ,just easy:
```Dart
void main() {
  dynamic a = 1;
  if (a < 2) {
    try {
      throw NBException();
    } catch (e) {
      print(e.errorString());
    }
  }
}

class NBException implements Exception {
  String errorString() => "This is a NBException";
}
```

Thanks.
