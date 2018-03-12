### Dart 内置类型

Dart提供了如下的几种数据类型:
- numbers
- strings
- booleans
- lists
- maps
- runes
- symbols

当然也可以使用字面量来声明变量的类型，比如:`this is a string`代表字符类型, `true`代表布尔类型，不过我们还是建议显式声明变量类型

由于每一个变量都是对于一个对象的引用，因此可以使用构造方法来初始化变量，例如`map`类型，就可以使用`new map()`来初始化一个`map`类型的变量

#### Numbers

`Numbers(num)`　包含两种子类型`int`和`double`这两种子类型只是数值范围和精度不同而已
`int`类型的值为整型，且取值范围为`-2^53`至`2^53`，　而`double`采用`IEEE 754`标准

对于`num`类型包含如下特性:

1. 包含一些基础的操作符,比如(`+, -, *, /`)
    ```dart
    int a = 3;
    int b = 4;
    int c;
    c = a * a + b * b;
    print(c);
    ```

1. 特殊方法，`abs, ceil, floor`等
    ```dart
    import 'dart:math';
    ...
    print(sqrt(c).ceil());
    ...
    ```

1. 定义在`int`类中的位操作符`<<, >>, &, |`
    ```dart
    int a = 3; //0011
    print(a >> 1); // 0001
    ```

1. 显式转为字符串
    ```dart
    int a = 3;
    print(a.toString());
    ```

 #### Strings(字符串)
 > Dart使用UTF-16字符集

1. 声明一个字符串可以使用单引号｀'｀,也可以使用双引号｀"｀
    ```dart
    // String s = ' this\'s a string';
    String s = 'this is a string';
    ```
1. 使用`${expression}`语法可以将一个值动态的插入到字符串中，如果需要插入的值简单，无需计算，则可以省略`{}`
    ```dart
      String s = ' this\'s a string';
    　print("this input type is string${s.toUpperCase()}");
    ```
1. 创建多行字符串，可以使用`'''`语法,这会按照多行，输出
    ```dart
      String s = '''
      You can create 
      Multi-line string like this one
     '''
    ```
1. 直接写多行，进行字符串的拼接
    ```dart
      String s = 'String '
      'Concatencation'
      " Works even over line breaks";
    ```
    以上会输出
    ```bash
    String Concatencation Works even over line breaks
    ```
1. 使用`+`进行字符串拼接
    ```dart
     String s = 'The + operator ' + 'Works, as well';
    ```

1. 不同数据类型的变量拼接,被拼接的变量只能是如下的类型:`num, string,bool`
    ```dart
    const aConstNum = 0;
    const aConstBool = true;
    const aConstString = 'a constant string';
    // const aConstList = const [1,2,3];
    String s = '$aConstNum $aConstBool $aConstString';
    ```

#### Boolean(布尔)
> 在Dart中，只有两种字面量`true, false`能够标识布尔值,而且只有`true`代表真，其他的所有值都表示`false`

#### List(列表)
> List在其他的语言中，通常称为数组，也就是某一种特定类型的集合，在Dart中称为List

用字面量来表达其类型如下:
```dart
List<int> list = [1,2,3,4];
```
以`List`加括号内代表类型的关键字作为一个整体来表示一个列表类型

对于一个列表来说，可以通过`length`属性来获取其长度，对于其中元素的访问也和其他语言一样，通过使用以`0`开始
的下标来访问其中的元素
```dart
List<int> list = [1,2,3,4];

print(list.length);

print(list[0]);
```
如果访问的下标越界，将会引发一个错误,并且下标不能为负数

通过使用`const`关键字，可以设置一个只读的列表
```dart
List<int> list = const [1,2,3,4];

print(list.length);

print(list[1]);

print(list[1] = 22); //Cannot modify an unmodifiable list
```

#### map
> 通常情况下，map表示的是k/v键值对的关联，其中k/v可以使任意的对象，在map中key必须是唯一的

用字面量表示其类型如下：
```dart
  Map<String, String> map = {
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
  };

  print(map);
  ```
以`Map`加括号内代表`key`与`value`类型的关键字作为一个整体来表示一个map类型

除了字面量，还可以使用构造函数累初始化一个map
```dart
  Map<String, String> map = new Map();
  map['first'] = 'partridge';
  map['second'] = 'turtledoves';
  map['fifth'] = 'golden rings';
  print(map);
```

对于一个map来说，可以通过`length`属性来获取其长度，对于其中元素的访问也和其他语言一样，通过使用以`key`来访问
如果`key`不存在，将会直接返回一个`null`

通过使用`const`关键字，可以设置一个只读的map
```dart
  Map<String, String> map = const {
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
  };

  print(map);
```

#### Runes
> 在dart中，runes是32位编码的字符串
Unicode为世界上所有的书写系统中使用的每个字母、数字和符号定义了一个惟一的数字值，而
Dart中是使用UTF-16编码来表示字符串，因此为了表示32位的Unicode值，对于多出的位数，
需要使用特殊的符号来填充

通常的Unicode字符的格式为`\uXXXX`,其中`XXXX`通常是四位十六进制的数字表示，如果位数大于或者小于4位
那么则需要使用花括号`{}`

在Dart的String类中，包含了一些有用的函数，用于转换

#### Symbols
 Symbols通常代表一个操作或者标识声明，也许很大程度上你并不会使用到它，但是在API的编写中，却非常有用
 这是因为:压缩的时候是变更变量的名称而不是其连接指向

 获取一个获取一个指向某个标识的symbol可以通过`#` 符号
 ```dart
 #radix
 #bar
 ```


