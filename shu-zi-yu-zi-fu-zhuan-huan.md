### 数字与字符串的装换

#### 字符串转数字

使用`parse`方法，可以经字符串转换为数字类型

```dart
assert(int.parse('42') == 42);
assert(double.parse('0.5') == 0.5);
assert(double.parse('1) == 1.0);
```

如果装换的类型为`num`而不是具体的`int`或者`double`类型，那么将会优先转换成`int`,如果不行，再转换成`double`

```dart
print(num.parse('1') == 1);
print(num.parse('1') == 1.0);
```

通过使用`parse`方法的第二个参数`radix`,可以设置字符串的进制

```dart
assert(int.parse('42', radix: 16) == 66);
```

#### 数字转字符串
使用`toString`方法可以将数字转换为字符串

```dart
assert(42.toString() == '42');
assert(123.456.toString() == '123.456');
```

使用`toStringAsFixed()`可以通过设置小数之后截取的位数，被截取的位数的后一位需要五舍六入

```dart
assert(123.456.toStringAsFixed(2) == '123.46');
assert(123.455.toStringAsFixed(2) == '123.45');
```

使用`toStringAsPrecision`可以指定数量的有效数字,该方法采取的是四舍五入的取舍进位方式
```dart
assert(125.457.toStringAsPrecision(2) == '1.3e+2');
assert(126.457.toStringAsPrecision(4) == '126.5');
```

