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
No complete.

Thanks.
