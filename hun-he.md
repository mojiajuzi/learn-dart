#### mixins(混合)

在继承中使用混合，提高了类代码的复用

一个类要想混合一个类，需要满足一下几点要求

1. 被混合类不能含有参数的构造方法

1. 使用`with`关键字的时候，前面必须使用`extends`关键字来实现继承




请看下面一个例子：
1. 先创建一个没有构造方法的被混合类
    
    ```dart
    class Music {
        String name;
        int palyerTime;
        final int _age = 10;

        void player(){
            print('this music ${this.name} play time is ${this.palyerTime}');
        }

    }
    ```

1. 然后定义被继承的父类
    ```dart
    class Book {
        String name;
        String author;

        Book(this.name, this.author);
        void read(){
            print('see.....');
        }
    }
    ```
1. 最后创建一个类用来继承和混合

    ```dart
    class Ebook extends Book with Music{


        Ebook(String name, String author):super(name, author){
            this.name = name;
            this.author = author;
        }

        void detail(){
            print('the book ${this.name} author is ${this.author}');
        }
    }
    ```

1. 最后在main函数中，我们可以如下进行调用
    
    ```dart
    main(List<String> args) {
        Ebook book = new Ebook("foods", "nothing");
        book.palyerTime = 100;
        book.player();
    }
    ```

Note:
1. 字段属性和方法属性将会被添加，就是继承一样，需要注意的是相同名称的属性，将会被覆盖

1. 混合了类，实例化该类的时候，这个类的类型也将属于被混合的类

    ```dart
        Ebook book = new Ebook("foods", "nothing");
        Book  book2 = new Ebook("foods", "nothing");
        Music  book2 = new Ebook("foods", "nothing");
    ```

1. 一个类可以混合多个类

    ```dart
    class A extends B with C, D {
        //
    }
    ```