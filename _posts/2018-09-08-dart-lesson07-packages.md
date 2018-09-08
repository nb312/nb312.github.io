---
layout: post
title: Dart 07 | Packages
subtitle: Packages and Libraries are told in this lesson.
tags: [dart,flutter]
---
# Library
We have been learning the basic concept in the pass lesson,but the knowledges are used in one file. if we want to use the other file in dart,we need the library.
### How to use a library
If you want use an exist library,you must use the keyword  `import`,the example is beneath.
```dart
import 'dart:math';

void main() {
  var a = 1;
  var b = 2;
  var m = min(a, b);
  print("m = $m"); //print  `m = 1`
}

```
Or Like this:
```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  var tP = TestPointer(1);
  print("isDown = ${tP.isDown}");
}
```
As we can see,the syntax of using a library is `import URL` or `import special library like 'dart:math'`,         
We import a library `math` here, for the library has been defined named 'dart.math' that we can use the name directly. If the library is not defined a name,then we can use this:
```dart
import 'package:io/io.dart';

void main() {
  copyPath("/home/nb/Workshop/FirstFlutter/second_flutter/test",
      "/home/nb/Workshop/FirstFlutter/second_flutter/tests");
}

```
The `io` library has not a name,so you can use them the URL of a file in the packages.the syntax is `import 'package: xxxLib/xxxLib.dart';`.Then it can be imported the `xxxLib` into the code that you can use it.
If you want to use the part of a library you can use the `show` or `hide` keyword,the `show` means that only the appointed part can be used.On the opposite side,`hide` means that the designation part is hided.the syntax like this `import 'package:lib_1/lib_1.dart' show A,B;` or `import 'package:lib_2/lib_2.dart' hide C,D;`,Examples are following:

##### Show   
If you call the copyPath,it is fine,but if you call the `copyPathSync`,there is an error `The function 'copyPathSync' isn't defined.`

```dart
import 'package:io/io.dart' show copyPath;

void main() {
  copyPath("/home/nb/Workshop/FirstFlutter/second_flutter/test",
      "/home/nb/Workshop/FirstFlutter/second_flutter/tests");
  copyPathSync("/home/nb/Workshop/FirstFlutter/second_flutter/test",
      "/home/nb/Workshop/FirstFlutter/second_flutter/tests");
}
```

##### Hide   

If you write like below,it will say there is an error `The function 'copyPath' isn't defined.`

```dart
import 'package:io/io.dart' hide copyPath;

void main() {
  copyPath("/home/nb/Workshop/FirstFlutter/second_flutter/test",
      "/home/nb/Workshop/FirstFlutter/second_flutter/tests");
}
```
### How to define a library
You can use the existing library above, but sometimes, you need custom a library by yourself.
In the path of `./animal` ,we create a file named  `Animal.dart`,contents are below:
```dart
void printAnimal() {
  print("This is an animal.");
}
```
Use them like this:
```dart
import 'animal/Animal.dart';

void main() {
  printAnimal(); //This is an animal.
}
```
If you want a prefix for the library,just like following:
```dart
import 'animal/Animal.dart' as animal;

void main() {
  animal.printAnimal(); //This is an animal.
}
```

# Packages
We learn to use the library above,but the library is already load in the packages,if you do not load it,how to use a package,the most important file you need to know is the `pubspec.yaml` file,which is in the root directory of a project.Let's see example in flutter project 'pubspec.yaml' file.
```yaml
name: second_flutter
description: A new Flutter application.

dependencies:
  flutter:
    sdk: flutter

  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^0.1.2

```
If you want to add a package,you need add it below the dependencies as the `flutter`,for example,if you want to `css_colors` package, you just need add like following:

```yaml

name: second_flutter
description: A new Flutter application.

dependencies:
  flutter:
    sdk: flutter

  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^0.1.2
  css_colors: ^1.0.0

```
Then click the `packages get` in the android studio ,or use the command line `pub get` in pure dart program or  the `flutter packages get` in flutter. If the package is installed completely,you can use them as a library ,which are used as the same as the above topics.
At present,we often use the `Git` tool to develop, the open sources of libraries are most in the Github,so we often need to load a library from the Github directly,the using is bellow.


`No Done`
     
