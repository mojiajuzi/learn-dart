#### Exception(异常)

> 异常表示程序没有按照设定的流程走，在Dart中使用`throw`抛出异常,`catch`捕获异常
> 与Java不同的是，在Dart中并不会对异常进行检查，也就是说方法并不会声明其是否会抛出异常

##### Throw
Dart提供了`Exception`和`Error`两种类型，当然还可以自定义异常，并且`throw`抛出的并不一定是异常
只要非空的对象，都可以使用`throw`抛出，例如：

```dart
throw new FormatException("Excepted at least 1 section");

throw 'Out of llamas!';

void distanceTo(Point other) => throw new UnimplementedError();
```

##### Catch
当程序抛出异常的时候，异常会阻止异常的传播，除非使用`rethrow`关键字

```dart
final foo = '';
main(List<String> args) {
  try {
     hello(); 
  } catch (e) {
     print('main() finished handling ${e.runtimeType}.');
  }
}

void hello(){
  try {
    foo = "world";
  } catch (e) {
    print("world");
    throw "throw exception";
  }
  print("hello function end");
}
```
以上程序在`hello`中强行对`final`属性的`foo`类型进行赋值操作,然后引发一个异常，并抛出一个字符类型的提示，然后我们得到如下的结果:

```
world
main() finished handling String.
```
也就是说，异常阻止了异常的传播，在`main`函数中捕获的是我们抛出的字符串，而是`hello`中捕获的异常
如果将`throw 'throw exception'`变更为`rethrow`,那么结果将会如下:

```
world
main() finished handling NoSuchMethodError.
```
也就是说，我们通过使用`rethrow`关键字将异常从当前的函数传递给了其调用者

为了对异常做更好的处理，可以使用多个`catch`的方式对不同的异常进行处理
```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}
```

当然在`catch`语句中，可以使用一个或者两个参数，如果只有一个的话，代表要抛出的异常，第二个参数代表调用的栈
```dart
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

不管是否抛出异常，为了做一些必要的工作，可以使用`finally`进行处理
```dart
void hello(){
  try {
    foo = "world";
  } catch (e) {
    print("world");
    throw "throw exception";
  } finally {
    print("hello function end");
  }
}
```


