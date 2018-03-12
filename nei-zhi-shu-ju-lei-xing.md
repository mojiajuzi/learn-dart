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


