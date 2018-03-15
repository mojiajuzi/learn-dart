#### Enum(枚举)

> 枚举是用来标识一个固定数量的静态变量的特殊类

定义一个枚举类型的时候，使用`enum`关键字

```dart
enum Color {
    red,
    green,
    blue
}
```

枚举类型中的每一个元素都有一个下标`index`, 下标按照定义时的顺序从`0`开始编号

```dart
print(Color.blue.index); //output 2
```

为了获取枚举类型的所有值，可以通过其`values`属性来访问

```dart
List<Color> colors = Color.values;
print(colors);
```

以上结果会输出
```
[Color.red, Color.green, Color.blue]
```

枚举类型可以被用在`switch`语句中

```dart
    Color c = Color.blue;
    switch (c) {
      case Color.red:
        print(Color.red.index);
        break;
      default:
        print(c.index);
    }
```

在enum中，以下几点需要注意

1. 枚举类型不能被extends(继承)，不能mix(混合),不能implement(实现) 
1. 枚举类型不能够被显示实例化