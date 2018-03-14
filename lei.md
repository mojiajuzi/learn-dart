### Class(类)

> Dart是单一继承的面向对象的语言，每一个对象都是类的一个实例，所有的类的都是`Object`类的继承类


#### 定义
一个类通常有两部分组成:方法属性(mehtod)和字段属性(data),因此我们可以定义如下的一个简单类

```dart
class Hello {
  String name;
  int age;

  void say(){
    print("the lang:${this.name} age is:${this.age}");
  }
}
```
如上我们定义了一个`Hello`类，它包含一个方法`say`, 两个存储数据的属性`name`,`age`,

方法的定义与函数的定义一样, 数据属性的定义与变量的定义一致

#### 构造方法
构造方法用于在一个类初始化成示例的时候，定义一些状态，定义构造方法，可以包含如下两种方法

1. 与类名相同

    ```dart
    Hello(String name, int age){
        this.name = name;
        this.age = age;
    }
    ```

1. 以`ClassName.constructName`的形式
    ```dart
    Hello.Java(int age){
        this.age = age;
        this.name = 'Java';
    }
    ```
Note: 以上我们为`Hello`定义了两个构造方法`Hello`和`Java`

#### 类的初始化

从一个类获取一个对象的时，使用关键字`new`, 和结构方法一样，获取类对象时也包含两种方式

1. 直接使用类名称
    ```dart
    Hello d = new Hello("Dart", 2);
    ```

1. 使用`className.ConstructName`
    ```dart
    Hello j = new Hello.Java(10);    
    ```
    
Note:对于构造方法拥有以下几个特性

- 如果一个类没有声明构造方法，那么将会使用默认的构造方法，只是这个方法没有参数并且在父类中调用
- 构造方法是不能继承的

默认情况下，子类的构造方法会在构造体中调用父类的构造方法，但是如果在子类的构造方法中使用了`initialize list(初始化列表)`那么调用的顺序如下:
- 初始化列表
- 父类无参数构造方法
- 当前类的构造方法
如果父类实现了自己的构造方法那么子类就必须使用其中的一个构造方法

类实例化以后，可以通过`'.'`访问实例中的数据和方法
```dart
Hello d = new Hello("Dart", 2);
print(d.name);
```

当然也可以通过`'.'`符号对实例属性进行赋值
```dart
d.name = "PHP";
print(d.name);
```

#### 类的继承
使用`extends`关键字，可以实现类的继承

```dart
class Book {
  String name;
  String author;
  int page = 0;
  
  void detail(){
    print('the book ${this.name} is  write by ${this.author} which page is ${this.page}');
  }
}

class Ebook extends Book {
  Ebook(String name, String author){
    this.name = name;
    this.author = author;
  }
}
```
以上，我们首先实现了一个`Book`类，然后我们创建一个新的类`Ebook`并通过`extends`关键字继承了这个类
这样我们新的类就包含了父类`Book`的属性和方法.

对于父类声明了构造方法而言，那么子类就必须选择其中一个来实现

1. 首先在父类中定义两个构造方法 

    ```dart
    Book(String name, String author){
        this.name = name;
        this.author = author;
    }

    Book.Page(int page){
        this.page = page;
    }
    ```

1. 那么在子类中，就必须选择其中的一个进行实现
    ```dart
    Ebook(String name, String author):super(name, author){
        this.name = name;
        this.author = author;
    }

    Ebook.Page(String name, String author, int page):super.Page(page){
        this.name = name;
        this.author = author;
    }
     ```

如果在一个类中设置了final属性的字段，那么就需要使用`initialize list`在函数构造函数开始之前执行

```dart

class Book {
  String name;
  String author;
  int page = 0;
  final bool review;
  
  Book(String name, String author, bool review):review=review{
    this.name = name;
    this.author = author;
  }

  void detail(){
    print('the book ${this.name} is  write by ${this.author} which page is ${this.page}');
  }
}

class Ebook extends Book {
  final bool  ebookreview;
  Ebook.Page(String name, String author, bool review):super(name, author, review), ebookreview = review{
    this.name = name;
    this.author = author;
  }
}
```

#### 重定向构造方法
重定向构造方法没有构造体，通过使用`:`跳转到其他的构造方法

```dart
main(List<String> args) {
  Dog d = new Dog.Alise("snoopy");

  print(d.age);
}

class Dog {
  String name;
  int age = 1;

  Dog(String name, int age){
    this.name = name;
    this.age =age;
  }

  Dog.Alise(String name): this(name, 2);

}
```

#### 静态构造方法

如果一个对象不会改变，那么可以通过实例化一个静态的实例化对象，因此类需要满足一下条件
- 创建一个静态的构造方法
- 所有的字段属性全部为`final`类型

```dart
main(List<String> args) {
  ImmutablePoint imm = const ImmutablePoint(1, 2);
  print(imm.x);
}

class ImmutablePoint {
  final num x,y;
  static final ImmutablePoint origin = const ImmutablePoint(0,0);
  const ImmutablePoint(this.x, this.y);
}
```

#### 工厂构造方法

使用`factor`关键字，可以相同的类实例，只需要实现一次
```dart
class Logger {
  final String name;
  bool mute = false;

  static final Map<String, Logger> _cache = <String, Logger>{};

  factory Logger(String name) {
    if(_cache.containsKey(name)){
      return _cache[name];
    } else {
      final logger = new Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);
  void log(String msg) {
    if(!mute) print(msg);
  }
}
```
以上类首先定义三个变量`name`, `mute`,`_cache`,其中`_cache`变量以String作为key, Logger作为类型的value组成的Map类型

然后增加了两个构造方法`Logger`,`_internal`(在Dart中私有的方法使用_标注)，
在Logger构造函数中，首先判断`_cache`中是否包含`name`多代表的值，如果有直接返回，如果没有就使用私有的`_internal`构造函数创建一个新的实例，并写入的`_cache`中

假如我们像如下进行调用:
```dart
  var logger = new Logger('UI');
  logger.log('Button clicked');
  var logger2 = new Logger('UI');
  logger2.log('Button clicked tow');
```
在上面就可以看到，以`UI`作为命名的Logger只创建了一次

#### Getters 和 setters

`Getters`和`setters`是获取、读取对象内容的特殊方法，通过使用`set`和`get`关键字，可以定义自己的getter和setter方法

```dart
class Rectangle {
  num left, top, width, height;
  Rectangle(this.left, this.top, this.width, this.height);

  num get right => left + width;
  set right(num value) => left = value - width;
}
```