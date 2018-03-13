### Function(函数)
> 在Dart中，函数也是一个对象并且属于`Function`类型，　因此函数也能够被赋值或者作为函数的参数进行传递

对于一个函数而言，其包含如下几个部分：
```dart
String sayHello(String name){
    return 'Hello' + name;
}
```

- String 返回值类型
- sayHello 函数名称
- String name: 参数列表
- `{...}` 函数体

Note: 
如果函数体仅仅是一个简单的表达式，那么函数体可以使用短语法
```dart
String sayHello(String name) => 'Hello'+ name;
```


#### 函数参数
对于函数的参数而言有两种类型：`必需参数(required)`，`可选参数(optional)`，其中必需参数应该是可选参数之前, 参数的类型，除了基本类型之外，还可以是`Function`等类型

可选参数可以选用如下两种形式来表达:

##### 名称
1. 使用`{param1,param2,....}`的形式定义一个名称的可选参数
    ```dart
    void enableFlags(String name, {bool blod, bool hidden}){
    //
    }
    ```
    
1. 调用的时候使用`paramName: value`的形式调用,使用命名参数，可以忽略参数的调用顺序
    ```dart
     enableFlags('Tom', hidden:false, blod: true);
    ```

##### 位置
1. 使用`[param1,param2]`的形式定义一个函数的未知可选参数
    ```dart
    void enableFlags(String name, [bool blod, bool hidden]){
    //
    }
    ```

1. 调用的时候，对于位置参数来说，传入的值按照定义的顺序依次赋值
    ```dart
    enableFlags('Tom', false, true);
    ```

##### 默认值
无论是命名参数还是未知参数，都可以使用`=`设置默认值，如果没有设置默认值，那么将采用类型的默认值`null`作为默认值
```dart
void enableFlags(String name, [bool blod = true, bool hidden]){
  //
}
```

#### main(主函数)
每一个应用都必须包含一个主函数，作为程序的入口，主函数的没有返回值，但是有一个List类型的参数，例如：
```dart
void main(List<String> arguments){
    //dosomething
}
```

#### 函数对象
将函数作为另外一个函数的参数进行传递
```dart
main(List<String> args) {
  List<int> list = [1,2,3];
  Function f = 
  list.forEach(printElement);
}

void printElement(int element){
  print(element);
}
```
以上定义了一个函数｀printElement｀，其功能非常简单，就是打印传递的参数`element`
然后在`list`中，将`printElement`作为参数传递

#### 匿名函数
绝大部门函数都包含函数名称，比如`main`, `printElement`函数，当然你也可以创建一个没有名称的函数，这样的函数我们称为:`匿名函数`

匿名函数和普通的函数的定义除了没有名称以外，其他部分都是相同的，例如我们可以使用匿名函数，改写`printElement`

```dart
List<int> list = [1,2,3];
list.forEach((int element) => print(element));
```

通常情况下，匿名函数也称为`lambda`,或者闭包(`closure`),既然涉及到闭包，那么就不得不说作用域问题

#### 作用域
首先看如下一个例子：
```dart
bool topLevel = true;
main(List<String> args) {
  bool insideMain = true;
  void myFunction(){
    bool insideFunction = true;
    
    void nestedFunction(){
      bool insideNestedFunction = true;
      print(topLevel);
      print(insideMain);
      print(insideFunction);
      print(insideNestedFunction);
    }
    nestedFunction();
  }
  myFunction();
  
}
```
如上定义了几个在不同作用域的变量，总的来说也就是两种作用域，`顶层作用域`，`函数作用域`
在顶层定义的变量，可以在全局范围之内访问，
```dart
void sayHello(){
  print(topLevel);
  // print(insideMain);  //这里会提示变量未定义
}
```

嵌套函数可以访问其父函数的变量,比如`nestedFunction`可以访问`myFunction`,`main`作用域之内的变量，但是反过来是不行的

#### 闭包
闭包是一个函数对象，当调用该函数的时候，其会保存其作用域之内的变量的状态,例如:
```dart
Function makeAdder(num addBy){
  return (num i) => addBy + i;
}

main(List<String> args) {
  Function add2 = makeAdder(2);
  Function add4 = makeAdder(4);
  print(add2(3));//打印结果为:5
  print(add4(3));//打印结果为:7
}
```

如上先定义一个`makeAdder`函数，其接受一个`addBy`参数，然后其消息体是一个匿名函数，该匿名函数接受一个`i`作为参数，在匿名函数之内执行`addBy + i`操作，由于`makeAdder`是匿名函数的父函数，因此在匿名函数内部可以访问父函数中定义的函数

然后在主函数中进行调用
```dart
Function add2 = makeAdder(2);
```
由于返回的是一个函数，然后再对返回的函数进行调用
```dart
add2(3);
```
由于`add2`会保存之前传递进入参数的状态，因此最后执行的结果为:5