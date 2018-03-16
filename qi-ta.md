### 类型定义(Typedefs)

在Dart中，函数也是一个对象就像字符串和数字也是字符串一样
使用`typedef`能够给一个函数定义一个新的类型，之后在其他的类型声明中就可以使用这种类型

考虑以下一段没有使用类型定义的代码:

```dart
class SortedCollection {
  Function compare;

  SortedCollection(int f(Object a, Object b)){
    compare = f;
  }
}

int sort(Object a, Object b) => 0;

main(List<String> args) {
  SortedCollection cool = new SortedCollection(sort);
  assert(cool.compare is Function);
}
```

以上代码首先定义一个`SortedCollection`类，在该类的构造方法定义了一个返回类型为:`(Object, Object)->int`的函数，并将该函数赋值给类型为`Function`的字段`compare`
以上代码的确定是显而易见的，那就是在赋值的时候，丢失了函数的类型信息，没有保留函数的信息

使用`typedef`改造如下:

```dart
typedef int Compare(Object a, Object b);

class SortedCollection {
  Compare compare;

  SortedCollection(this.compare);
}

int sort(Object a, Object b) => 0;

main(List<String> args) {
  SortedCollection cool = new SortedCollection(sort);
  assert(cool.compare is Compare);
}
```
我们使用`typedef`定义了一个类字段`compare`所需要的类型`(Object, Object) -> int`，
之后我们为类字段定义的时候，就可以直接使用`Compare`类型


由于`typedef`是简单的别名，因此常常用来做判断类型

```dart
typedef int Compare<T>(T a, T b);

int sort(int a, int b) => a-b;

main(List<String> args) {
  assert(sort is Compare<int>);
}
```

#### 元数据(metadata)

使用元数据可以给代码增加额外的信息，而不会改变代码的逻辑
使用元数据则以`@`符号开头，后面跟着一个静态常量或者静态的构造方法

`@override`，`@deprecated`两个元数据可以用于全局

```dart
class Television {
  void turnOn(){

  }

  @deprecated
  void activate(){
    turnOn();
  }
}
```

当然，也可以定义元数据结构
首先在一个`todo`库中，定义一个类

```dart
library todo;

class Todo {
  final String who;

  final String what;

  const Todo(this.who, this.what);
  
}
```

然后在另外一个包中引入并使用

```dart
import "todo.dart";

@Todo('seth', 'make this do something')
void doSomething(){
  print('do something');
}
```

元数据能够出现在库，类，类型定义，类型参数，构造函数，工厂，函数没字段没参数，变量声明之前，或者导入，导出指令之前，

使用反射，就可以在运行的时候得到元数据

#### 注释
Dart允许三种方式的注释
- 单行注释
- 多行注释
- 文档注释

#### 单行注释
单行注释使用`//`开头，后面添加注释

```dart
class Book {

  void detail(){
    //TODO: print the book detail
  }
}
```

#### 多行注释
多行注释使用`/**`开头，以`*/`结尾

```dart
/**
 * @params num price 单价
 * @params num count 数量
 */
  num totalPrice(num price, num count){
    return price * count;
  }
```

#### 文档注释
文档注释使用`///`开头

```dart
class Book {
  ///数据名称
  ///字符串类型
  ///...
  String name;

  String author;
  void detail(){
    //TODO: print the book detail
  }


/**
 * @params num price 单价
 * @params num count 数量
 */
  num totalPrice(num price, num count){
    return price * count;
  }
}
```