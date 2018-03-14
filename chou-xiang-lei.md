#### Abstract class(抽象类)
使用关键字`abstract`可以声明一个类为抽象类，在类中没有方法体的方法称为抽象方法,抽象方法不能够被实例化

```dart
abstract class Animal {
  void voice();

  void food(){
    print("~~~");
  }
}
```

通过使用关键字`extends`可以继承一个类，继承这个类的时候，必须实现其中的抽象方法

```dart
class Dog implements Animal {
   void voice(){
     print('wang~wang~~~');
   }

   void food(){
     print('bone');
   }
}
```

然后我们就可以进行如下的调用

```dart
main(List<String> args) {
  Animal dog = new Dog();
  dog.voice();
  dog.food();
}
```
在这里有一点需要注意的是下面条语句

```dart
Animal dog = new Dog();
```
这么我们看到一个类继承了一个抽象类，那么其实例也属于该类型，也就是说，一个抽象类就相当于定义了一种类型

#### 隐式接口
每一个类都隐式定义了一个接口，该接口包含实例的所有成员以及所有接口的实现，
如果你想创建一个类A,该类拥有B类的所有接口，但是却不包含接口的实现，这个时候就适合使用实现而不是继承

1. 首先定义一个`Person`类，该类包含一个私有属性`_name`，一个与类名同名的构造方法，以及一个`greet`方法
    ```dart
    class Person {
        final _name;
        Person(this._name);
        String greet(String who) => 'Hello, $who, i am $_name';
    }
    ```

1. 然后再定义另外一个类来实现
    ```Dart
    class Impostor implements Person {

        String greet(String who) => 'Hi $who, Do you know who i am?';
    }
    ```

1. 接着调用一下`Impostor`

    ```dart
    main(List<String> args) {
        print(greetBob(new Person('Kathy')));
        print(greetBob(new Impostor()));
    }
    String greetBob(Person person) => person.greet('Bob');
    ```

Note:
在Person中，由于`Person()`是构造方法，`_name`是私有方法，所以`Person`类只有`greet`一个接口是公开的

因此`Impostor`类，只需要实现其`greet`方法即可,如果这个时候通过其实例对象调用其不存在的属性`_name`时

```dart
  Person imp = new Impostor();
  print(imp._name);
```
这个时候会提示，`_name`不是`Impostor`的接口,在这种情况下，我们可以使用`getters`的方式，返回一个结果

```dart
  get _name => '';
```

到这里，我们基本可以看到,`extends`和`implements`的一些差别:

1. 一个类的接口分为两类，公开接口和私有接口

1. 通过`implements`的方式，只能拥有公开接口，而不能获取私有接口

1. 如果是类含有参数的构造方法，那么继承将会需要实现该构造方法

对于一个类来说，可以同时实现多个类的接口，只需要像如下调用即可：
```dart
class A implements B, C {
  //todo
}
```