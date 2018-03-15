#### static(静态属性与方法)

##### 静态属性

在类中定义一个静态的属性，只需要使用关键字`static`即可

```dart
class Book {
  static const bool review = true;

  static  String color = 'blue';
}

main(List<String> args) {
  Book.color = "Yellow";
  print(Book.color);
  print(Book.review);
  
}
```
以上会打印出

```dart
Yellow
true
```

在类中定义了静态属性之后，可以通过`ClassName.Field`的形式进行调用,
注意`review`和`color`属性的区别，如果没有使用`const`关键字定义一个常量，那么其值可以在外部被改变,这是非常不可取的做法，因此，定义一个静态属性的时候，我们通常将其定义为常量

静态属性在调用的时候才会被初始化

##### 静态方法

使用`static`关键字可以定义一个方法为静态方法，对于一个静态方法的访问与访问静态属性是一样的，即使用`ClassName.staticMethodName`的形式，但是有一点需要注意的是在静态属性中没有`this`对象

```dart
import 'dart:math';

class Point {
  num x,y;
  Point(this.x, this.y);

  static num distanceBetween(Point a, Point b){
      num dx = a.x - b.x;
      num dy = a.y - b.y;
      return sqrt(dx * dx + dy * dy);
  }
}

main(List<String> args) {
  Point a = new Point(2, 2);
  Point b = new Point(4, 4);

  print(Point.distanceBetween(a, b));
}
```