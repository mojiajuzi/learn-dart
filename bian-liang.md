### Dart 变量

#### 变量的声明
> 所有未初始化的变量都包含一个默认的初始值`null`, 即使是数字类型，因为在Dart中一切皆对象

Dart的变量声明主要有三种方式，分别对应`var`, `const`, `final`

```dart
main(List<String> args) {
  var a = "a";
  final b = "b";
  const c = "c";
}
```
当然，变量声明的时候，建议添加变量的类型

```dart
var a = "a";
// or String a = "a";
final String b = "b";
const String c = "c";
```
这里有一点需要注意的是：在声明并初始化`var`关键字后面无法添加类型

#### 差异
- var: 常规变量，可重复赋值
- final: 只能赋值一次
- const: 常量，只能初始化时赋值

##### Final
1. 在非类属性或者顶部(函数或者类之外)声明的时候，必须初始化，且初始化之后无法进行赋值
```dart
main(List<String> args) {
  final String name = 'Tom';
  name = "Bob"; //这里会编译不过去
}
```

1. 如果是类属性或者顶层，可以先声明，然后再赋值
```dart
main(List<String> args) {
  var h = new Hello("Tom");
  print(h.name);
}

class Hello {
  final String name;

  Hello(String inputName):name = inputName;
}
```

##### const
`const`不仅仅可以用来创建常量，也可以创建常量的值
```dart
const hello = [];
hello = []; //运行出错
```
初始化之后，只能读取`hello`中的值，而不能对变量`hello`做其他的操作，比如:写