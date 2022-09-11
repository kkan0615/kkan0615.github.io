---
title: 5 ways to remove element in dart
author: Youngjin Kwak
date: 2022-09-09 22:21:00 +0800
categories: [dart]
tags: [dart]
image:
  path: ../images/dart-logo.jpg
  width: 800
  height: 500
  alt: dart-logo.
---
---
# Overview
This post is written under Dart 2.18. You can test all the codes on [DartPad](https://dartpad.dev/?)

# 1. removeAt(): Remove element at a specific index
```dart
E removeAt(int index);
```
## Note
```removeAt()``` method can remove an element at a specific index in the list.
```removeAt()``` method takes an int type argument and returns the removed element.
```removeAt()``` method reduce size of list by one. [Document](https://api.dart.dev/stable/2.13.4/dart-core/List/removeAt.html) is here.
## Example
```dart
 List list = [1, 2, 3, 4, 5];

 int removedElement = list.removeAt(1);

 print(removedElement);  // Expect: 2
 print(list);            // Expect: [1, 3, 4, 5]
 print(list.length);     // Expect: 4
```

# 2. remove(): Remove specific element
```dart
bool remove(Object? value);
```
## Note
```remove()``` method can remove an element from the list. If there are same element in the list, first element will be removed. ```remove()``` takes a value which will be removed.
```remove()``` returns boolean type of result. If the specific element is removed successfully, ```remove()``` method will return "true".
Otherwise, ```remove()``` method will return false if the element is failed to removed by some reasons such as the element is not existed.
```remove()``` method reduces the size of list by one if it's success.
[Document](https://api.dart.dev/stable/2.13.4/dart-core/List/remove.html) is here.
## Example
```dart
 List list = [1, 2, 3, 4, 5];

 bool isSuccess = list.remove(1);
 bool isFail = list.remove(8);

 print(isSuccess);       // Expect: true
 print(isFail);          // Expect: true
 print(list);            // Expect: [2, 3, 4, 5]
 print(list.length);     // Expect: 4
```

# 3. removeLast(): Remove last element from list
```dart
E removeLast();
```
## Note
```removeLast()``` method removes the last element from the list. ```removeLast()``` does not take any argument.
```removeLast()``` returns the removed element.
However ```removeLast()``` occurs an error if the list is **not empty**.
```removeLast()``` reduces size of the list by one if there is removed element.
[Document](https://api.dart.dev/stable/2.13.4/dart-core/List/removeLast.html) is here.

## Example
```dart
 List list = [1, 2, 3, 4, 5];

 int removedElement = list.removeLast();

 print(removedElement);  // Expect: 5
 print(list);            // Expect: [1, 2, 3, 4]
 print(list.length);     // Expect: 4
```

## Error Message
```
Uncaught Error: RangeError (index): Index out of range: index must not be negative: -1
```

## Alternative
Along with ```removedAt()``` method which is mentioned above and length of list as an argument, ```removeAt(List.length - 1)``` is an alternative way.
```dart
 List list = [1, 2, 3, 4, 5];

 int removedElement = list.removeAt(list.length - 1);

 print(removedElement);  // Expect: 5
 print(list);            // Expect: [1, 2, 3, 4]
 print(list.length);     // Expect: 4
```

# 3.1 Remove many last elements from list
Developers are allowed to remove multiple last elements from list with ```List.length``` property.
Easily developers change the length to new length.
However, new length should be **positive number**.
You also can remove elements by subtracting specific number which is less than length

## Example
```dart
 List list = [1, 2, 3, 4, 5];

 int newLength = 3;
 list.length = newLength;

 print(list); // Expect: [1, 2, 3]
 print(list.length); // Expect: 3
```
## Example 2
```dart
 List list = [1, 2, 3, 4, 5];

 list.length = list.length - 2;

 print(list); // Expect: [1, 2, 3]
 print(list.length); // Expect: 3
```

# 4. removeRange(): Remove element between specific number and specific number
```dart
void removeRange(int start, int end);
```
## Note
```removeRange()``` method is good for removing many elements in range.
```removeRange()``` takes two arguments. First argument is for start and last argument is for end.
end should be same or greater than start.
end and start should be smaller than the list's length.
```removeRange()``` reduces the list's length by **end - start** which is taken as arguments.
Return type of ```removeRange()``` is **void**

## Example
```dart
List list = [1, 2, 3, 4, 5];

list.removeRange(2, 4);

print(list); // Expect: [1, 2, 5]
print(list.length); // Expect: 3
```

# 5. removeWhere(): Remove specific element by passing function which returns boolean type
```dart
void removeWhere(bool test(E element));
```
## Note
```removeWhere()``` method remove all elements matched by condition.
```removeWhere()``` takes a function argument which has boolean as return type.
The return type of ```removeWhere()``` method is void.

## Example
```dart
  List list = [1, 2, 3, 4, 5];

  list.removeWhere(((element) => element > 3));

  print(list); // Expect: [1, 2, 3]
  print(list.length); // Expect: 3
```

# Ref
- https://api.dart.dev/stable/2.13.4/dart-core/List-class.html#instance-properties

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
