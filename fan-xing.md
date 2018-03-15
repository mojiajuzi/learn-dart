### Generics(泛型)

如果你去查看基础的数组类型`List`的API文档的时候，你可以看到它实际的类型为`List<E>`，　其中`<...>｀标识一个泛型
为了表达方便，通常泛型的具体类型使用单个字母标识，比如:`E,T,S,K,V`等

由于在Dart1.x版本中，类型声明是可选的，所以你可以使用也可以不使用，为了使代码更加清晰，准确，这里强烈建议添加类型声明

例如，你想创建一个元素只包含字符串类型的列表，你可以这样声明`List<String>`，通过这种方式，如果你添加了非字符串类型的元素
你的IDE会进行提示

```dart
  var names = new List<String>();
  names.addAll(['Seth', 'Kathy', 'Lars']);
  names.add(24);
```

另外使用泛型能够减少代码数量，尤其是在可以使用接口，继承等特性的时候，比如一下一个例子：

1. 假设你需要创建一个对象缓存的类
    
    ```dart
    abstract class ObjectCache {
        Object getByKey(String key);
        void setByKey(String key, Object value);
    }
    ```
    
    在这个类中包含两个方法，一个是通过一个string类型的参数，获取存储的对象，另外一个是通过string类型的参数和作为值的`Object`对象

 1. 然后你需要一个字符串缓存的类

    ```dart
    abstract class StringCache {
        String getByKey(String key);
        void setBykey(String key, String value);
    }
    ```
    
    该类和存储对象的类拥有相同的两个方法，而且仅仅只是存储的对象不同而已，因此，我们可以使用泛型来进行改造

1. 改造的方向是将具体的类型隐藏起来，通过使用抽象的类型来替代

    ```dart
    abstract class Cache<T> {
        T getByKey(String key);
        void setByKey(String key, T value);
    }
    ```
    
这样，不论创建多少种不同类型的存储类，我们都可以通过继承`Cache`类来进行实现


##### 字面量集合
List和Map类型，可以通过在声明的时候，添加元素类型标识来声明和限制保存的元素类型

```dart
  var pages = <String, String>{
      'index.html':'Homepage',
      'robots.txt':'Hints for web robots',
      'humans.txt': 'we are people, not machines'
  };
```
以上通过使用`<String, String>`来标识这个`Map`的key类型为:`string`, value的类型为:`string`

对于List也是一样的用法

```dart
var names = <String>['Seth', 'Kathy', 'Lars'];
```

##### 构造方法添加类型声明

```dart
  var names2 = new List<String>();
  names2.addAll(['Seth', 'Kathy', 'Lars']);
```
当我们初始化一个List类型的时候，我们添加`<String>`来表明，所创建的`List`存储的元素类型为`string`类型


##### 泛型包含类型判断

在Dart中，泛型的类型是具体的，也就是说在运行的时候，泛型所代表的必定是某一个具体的类型，可以获取其具体的类型信息

```dart
var names = new List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
```
然而需要注意的是，`is`表达式只是检查其集合类型，并不会检查其对象内部,因此在生产环境中比较好的做法是检查每一个元素类型或者使用异常来处理

##### 类型限制
在实现一个接口泛型的时候，可以通过参数来限制参数的类型

1. 首先定义两个类`Book`和`Ebook`,其中`Ebook`类继承了`Book`

    ```dart
    class Book {
        //todo
    }

    class Ebook extends Book {
        //todo
    }
    ```

1. 创建一个新类，这个类中对类型进行了限制，只能是`Book`类型
    
    ```dart
    class Foo<T extends Book> {
        //todo
    }
    ```

1. 然后在main函数中进行调用

    ```dart
    var foobook = new Foo<Book>();
    var fooebook = new Foo<Ebook>();
    var fooobject = new Foo();
    ```

可以看到，尽管`Foo`类中对于泛型`T`的类型进行了限定，只能是`Book`类型，但是由于`Ebook`继承了`Book`类型，因此他也属于`Book`类型

