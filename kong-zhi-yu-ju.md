#### Dart中的流程控制语句

在Dart中，包含了如下几种历程控制语句

- if....else
- for
- while....do-while
- break
- continue
- switch....case
- assert

当然，通过使用`try-catch`和`throw`语句可以变更程序的流程

##### if-else

```dart
if(isString()){
    //todo
}else if(isBoole()){
    //todo
}else{
    //todo
}
```

##### for

```dart
main(List<String> args) {
  List<Function> callbacks = [];

  for (var i = 0; i < 2; i++) {
    callbacks.add(()=>print(i));
  }
  callbacks.forEach((c)=>c());
}

以上代码我们定义了一个元素类型为函数的列表

```dart
  List<Function> callbacks = [];
```

然后使用一个`for`循环语句，往列表中添加一个匿名函数。该匿名函数的功能仅仅是打印循环的次数，因此使用段语法

```dart
  for (var i = 0; i < 2; i++) {
    callbacks.add(()=>print(i));
  }
```

对于可迭代的类来说比如List和Set，如果不需要其下标，那么可使用`for-in`语法来遍历整个对象

```dart
  List<int> collection = [1,2,3];
  for (var x in collection) {
    print(x);
  }
```

##### while与do-while

`while`与`do-while`的最大区别就是是否执行的问题

```dart
main(List<String> args) {
  bool a = true;

  while(!a){
    print('while');
  }

  do {
    print('do-while');
  } while (!a);
}
```
以上输出结果为`do-while`,这就是两者最明显的区别，`while`是先判断后执行，`do-while`是先执行后判断

##### break 和 continue
`break`和`continue`都是用来中止程序的执行，但是它们的效果程度不一样，
`break`结束整个循环，`continue`终止循环，开启下一次循环

```dart
  List<int> list = [1,2,3,4];

  for (var i = 0; i < list.length; i++) {
    if(list[i] % 2 == 0){
      continue;
      //break;
    }
    print(list[i]);
  }
```
如果使用的是`continue`，以上程序将会输出`1,3`,相反，如果使用的是`break`,那么只会输出`1`


##### switch....case
`switch`语句使用`==`运算符来比较`integer, string,const`类型是否相等，被比较的两个对象必须是相同的类型，
就算是子类型也不行，一个switch语句的机构如下:
```
switch (statement){
    case :
        break
    default:
}
```
`switch`语句中，将statement与case语句的值进行比较，`case`后面添加`:`然后跟随的是符合条件时需要执行的语句，
当`case`语句结束后，需要添加一个`break`语句，表示结束这个循环

```dart
main(List<String> args) {
  String a = "Java";
  switch (a) {
    case 'PHP':
      print('php');
      break;
    case 'Java':
      print('Java');
      break;
    default:
      print("Dart");
  }
}
//putout: Java;
```

如果case语句里面包含了代码逻辑，而没有使用`break`，将会提示错误，但是如果没有代码逻辑，也就是为空，却是可行的

```dart
  String a = "Java";
  switch (a) {
    case 'PHP':
      print('php');
      break;
    case 'kotlin':
    case 'Java':
      print('Java');
      break;
    default:
      print("Dart");
  }
```

通过设置类似于锚点的方式，可以使得程序忽略对`case`语句的判断，直接执行该语句内的代码逻辑

```dart
  String a = "Java";
  switch (a) {
    case 'PHP':
      print('php');
      break;
    case 'Java':
      print('Java');
      continue Javascript;

    Javascript:
    case 'Javascript':
      print('Javascript');
      break;
    default:
      print("Dart");
  }
```
以上代码将会输出`Java`和`Javascript`

##### assert
当条件判断语句为false的时候，`assert`语句能够破坏程序的正常执行

```dart
  String a = "Java";
  String text;
  
  assert(text != null);
  print(a);
```
