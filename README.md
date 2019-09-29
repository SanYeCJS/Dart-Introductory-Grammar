# Dart语法一天快速入门篇 (Github发布版本)

> 针对当下热门的Flutter跨平台开发语言，Dart语法是其根本，所以这里写了一篇关于Dart语法的文章，希望可以帮到各位快速入门Dart，觉得还不错的朋友麻烦动动手指头给个star支持下原创作教程，后续会出其他更多相关的开发教程
 
* 作者：SanYeCJS 
* github地址：https://github.com/SanYeCJS/Dart-Introductory-Grammar

## 环境安装篇

### Dart本地环境安装（Mac）
>如果本地还没安装homebrew的，需要先安装：
[Homebrew 安装地址](https://brew.sh/)

`brew tap dart-lang/dart` <br>
`brew install dart` <br>

升级版本 `brew upgrade dart`

vscode 需要安装 code runer 和 dart 两个插件

## 类型
>Dart是强大的脚本类语言，可以不定义变量类型使用var字段(类似JavaScript)，系统会自动推导该变量类型
好比 var str = 'hello world' 也可以用 
String str = 'hello world' ,
var a = 1和 int a = 1 

### 常量修饰符final和const
>const表示值不变，并且一开始就需要赋值
>final也表示该值不能修改，但可以初始化不赋值，但是只能赋值一次

**示例代码**

`final a = new DateTime.now();
 print(a);` <br>
 `const b = new DateTime.now();
 print(b);`
 
### 数值类型 String bool List Map类型分析
* String（定义） 可以用三个单引号或者双引号，可以对字符串进行换行调整，输出到控制台还是会按照定义的方式输出，单引号或双引号的不能这么输出

* String(输出格式,例如str1= 'a', str2= 'b') 可以使用print('$str1  $str2');
输出结果`a b`,另一种拼接方式，可以直接用+号，例如 print(str1 + str2)

* 数值类型包括int,double
* bool取值true、false （1或者任何非null类型的都为true）

* List,列表相对来说是支持动态操作的，增（add）,删（removeAt）,改（list[0]=null），长度（length属性）,插入（insert(index, element)）
* List支持定义泛型，例如`var list = new List<String>();`

* Map类型，可以直接用var定义，同样支持泛型定义， 例如`var map = new Map<String, int>();`


### 类型判断 is  和 ？？= 和isEmpty
>判断是否是某个类型的值,   xx is 类型名称

>??=  如果左边的类型是null ,则将右边的值赋值给左边， 好比 int a;  a??=10;  a的最终结果就是10

>isEmpty判断字符串是否为空串，如果判断对象是null会报错，例  str.isEmpty(属性不是方法)
 
### 类型转换
 * Number转String使用toString()
 * String转Number使用 parse()

## Dart常用属性以及方法
#### 属性
* length
* reversed (倒序列表，输出对象是元组)
* isEmpty
* isNotEmpty 
* keys  获取所有的key值 （主要用在字典上）
* values 获取所有的value值（主要用在字典上）


#### 方法
* toList() 将list对象转List
* addAll() 拼接数组
* indexOf()  查到返回索引值，查不到返回-1
* removeAt()  删除指定索引
* join()   将列表以特定符号拼接成一个字符串
* split()  将字符串以特定符号转成list
* containsValue()  是否包含某个值


## 循环方式
### foreach

示例

```
  var list = ['1','2', '3'];
  var map = {'name':'zhangsan','age':10};

  list.forEach((value){
    print("value is $value");
  });

  map.forEach((key,value){
    print("key is $key , value is $value");
  });

```

### map 
>说明 ：对list中的元素统一操作，例如统一加减乘除等

**示例代码**

```
var li = [1, 3, 5];
var newLi = li.map((value){
  return value*2;
});
print(newLi);
```

### where条件

**示例代码**

```
var li = [1, 3, 5];
var newLi = li.where((value){
  return value >= 3;
});
print(newLi);
```

### any条件
>说明：判断是否对象当中有某个条件成立即返回true，好比列表中大于6的元素是否存在

**示例代码**

```
var li = [1, 3, 5];
var flag = li.any((value){
  return value >=6;
});
print(flag);
```

## 函数
> 注意：函数的形参可以不指定类型，返回值也是可以不指定的，但是为了规范写法，一般还是带上特定的类型做修饰，例如无返回使用关键字 void，形参用强类型限定防止外部参数传入任意类型导致出错。

* 可选参数 printInfo(String username, [int age]);
可选参数一般放最后

* 默认参数 printInfo(String username, [sex='男']);

* 将方法作为参数传给函数(其实也类似与匿名函数，参考代码片段二)
 
代码片段1

```

void fn(){
  print('fn invoke');
}

void fn2(fnName) {
  fnName();
}

main() {
  fn2(fn);
}
```

代码片段2

```
var fn = (){
  print('hello world');
};

main() {
  fn();
}
```

* 如果函数的方法体只有一句代码，可以用=>代替花括号,以下例子用forEach，例如：

```
main() { 
  var list = ['zhangsan', 'lisi', 'wangwu'];
  list.forEach((value)=>print(value));
}

```

### 自执行函数
>说明：实际为匿名函数自己调用

```
  ((){
    print('123');
  })();
```


## 闭包
> 特点：能使变量常住内存并且不会污染全局，既有全局变量的特点也有局部变量的特点

```
main() {
  func(){
    int a=100;
    return (){
      a++;
      print(a++);
    };
  }

  var func2 = func();
  func2();
  func2();
  func2(); 
}
```

## 类
### 初始化声明
> 可以在生成对象的同时初始化内部参数，如下代码片段：

```

class Rect {
  int width;
  int height;

  //初始化参数
  Rect():width=10,height=10{}
  
  get area {
    return this.width * this.height;
  }

  set areaWidth(int width) {
    this.width  = width;
  }

}

main() {
  Rect rect = new Rect();
  print(rect.area);
}
```

**Flutter中生成对象通常会省略new关键字，如下代码片段**

```
var rect = Rect();

//类似flutter中返回widget
return Center();//此处省略了new关键字

```

### 默认构造函数
>  默认构造函数跟类名一致，如下代码片段：

```
class Person{
  String name;
  int age;

  //默认构造函数(只能存在一个默认构造函数)
  Person(String name, int age) {
    this.name = name;
    this.age  = age;
  }
}
```

以上代码可以简写为如下：

```
class Person{
  String name;
  int age;

  //默认构造函数(只能存在一个默认构造函数)
  // Person(String name, int age) {
  //   this.name = name;
  //   this.age  = age;
  // }
  
  //默认构造函数简写
  Person(this.name, this.age);
}
```
### 命名构造函数 
> 一个类写多个命名构造函数，写法如下：

```
class Person{
  String name;
  int age;

  Person.now(String name, int  age) {
    this.name = name;
    this.age  = age;
  }

  Person.now2(String name, int  age) {
    this.name = name;
    this.age  = age;
  }
}

main() {
  Person p = new Person.now('zhangsan', 10);
  Person p2 = new  Person.now2('lisi', 11);
}
```

### 类内部的函数中访问类属性

```
class Person{
  String name;
  int age;

  void printInfo(){
    //通过${this.xxx}
    print('${this.name} , ${this.age}');
    
    //通过this.xxx
    print(this.name);
    
    //通过$name
    print('$name');
  }
}
```
### 对象操作符

* ？条件运算符（如果为空，后续操作不执行，例如p为null，调用getInfo方法，政策执行会报错，如果加上p?.getInfo()就不会调用了）,示例代码如下：

```
var p;

//这里调用报错，因为p为null
p.getInfo();

//进行非空判断,不会执行getInfo方法 
p?.getInfo();
```

* as 类型转换

**示例代码**

```
class Person {
  Person(){}

  void printInfo(){
    print("person test");
  }
}

main(){
  var p;
  p = '';
  p = new Person();
  
  (p as Person).printInfo();

}
```


* is 类型判断（参考以上【类型】章节的讲解第三点）

* ..  级联操作（连缀,这种语法类似于链式方式）

```
class Person {
  String name;
  int age;
  Person(){}

  void printInfo(){
    print("person test");
  }
}

main(){
  Person p = new Person();
  p..name = 'zhangsan'
   ..age  =  10
   ..printInfo();
}
```

### 继承
#### 关键字extends
例如 `class Teacher extends Person{}` 表示Teacher类继承自Person类 
#### 调用父类默认的方法 super

```
class Teacher extends Person {
    //此方式调用父类的默认构造方法
    Teacher(String name, int age): super(name,  age);
}
```
#### 重写父类方法 @override(可以不加，但是一般会加上)

```
 class Person {
  void printInfo(){
    print("person test");
  }
}

class Teacher extends Person{

  //采用关键字@override 标记该方法是重写父类的，这点跟Java一样
  @override
  void printInfo() {
    super.printInfo();
  }
}
```

### 抽象类
>Dart中的抽象类主要用于定义标准，这个跟Java语言有点像，在Dart中，抽象类也可以作为抽象类接口来使用， 抽象类通过关键字 abstract来定义，如果想作为接口来使用定义一套标准，可以用关键字 implements来使用

#### 抽象方法 
* Dart中，抽象方法不能用abstract来修饰，抽象类中没有方法体的方法我们可以称之为抽象方法
* 如果子类继承抽象的父类就必须实现里面的所有抽象方法（也可以说是重写所有父类抽象方法，这里记得是抽象方法，抽象类可以存在非抽象方法）
* 如果把抽象类作为接口来使用，就必须实现所有抽象类里面定义的所有属性与方法
* 抽象类不能直接被实例化，只要子类才可以
* 接口更多用于约束和规范，而抽象类更多用于共用某些方法

**示例代码**

```
//抽象类 继承的子类必须实现抽象方法
abstract class A {
  printA();

  printAA(){
    print("AA");
  }
}

//接口 实现该接口必须实现 方法+属性
abstract class B {
  String name;
  printB();
}


class C extends A implements B {
  @override
  String name;

  @override
  printA() {
    print('A');
  }

  @override
  printB() {
    print('B');
  }
}
```

### mixins
> Dart中有一种方式能实现类似多继承，但实际不是继承,用关键字with

**示例代码**

```
class A {
  void printA(){

  }

  void getStr(){
    print("this is A method");
  }
}

class B {
  void printB(){

  }

  void getStr(){
    print("this is B method");
  }
}

class C with A, B {
  @override
  void printA() {
    print("重写的A方法");
  }

  @override
  void printB() {
    print("重写的B方法");
  }
}

void main() {
  C c = new C();
  c.printA();
  c.printB();

  //A和B均有getStr 方法，调用哪个方法取决于with之后写的顺序有关，最后一个会覆盖前面所有的
  c.getStr();  

  print(c is A);  //true 
  print(c is B);  //true
}
```

## 访问修饰符
### 私有属性和方法
> Dart中没有像Java语言中有public，private，protected这些访问修饰符，但是我们可以采用下划线_ 把一个属性或者方法定义成私有的，这一点跟Python的语法很像，但是应该注意的一点，当把该声明了私有方法或属性单独抽离为一个文件时，才生效，好比把Person类放在model目录下，然后其他文件引用了这个model，才变成不能访问的私有属性和方法

### getter和setter修饰符

以下是最原始的代码片段：

```

class Rect {
  int width;
  int height;

  Rect(this.width,  this.height);
  
  // 简单地求面积
  int area() {
    return this.width * this.height;
  }

}

main() {
  Rect rect = new Rect(10, 2);
  print(rect.area());
}
```

#### get 关键字修饰

```

class Rect {
  int width;
  int height;

  Rect(this.width,  this.height);
  
  // 简单地求面积 通过添加get修饰符，可以把area函数变为属性的访问方式
  get area {
    return this.width * this.height;
  }

}

main() {
  Rect rect = new Rect(10, 2);

  //这里通过属性的访问方式调用方法 
  print(rect.area);
}
```
#### set 关键字修饰

```

class Rect {
  int width;
  int height;

  Rect(this.width,  this.height);
  
  // 简单地求面积 通过添加get修饰符，可以把area函数变为属性的访问方式
  get area {
    return this.width * this.height;
  }

  set areaWidth(int width) {
    this.width  = width;
  }

}

main() {
  Rect rect = new Rect(10, 2);
  rect.areaWidth = 100;
  //这里通过属性的访问方式调用方法 
  print(rect.area);
}
```

## static 
>① 说明: 通过static修饰的属性和方法，外部可以通过类名直接调用，例如：
`Person.name`  `Person.getInfo()`

>② static修饰的方法不能访问非static修饰的属性

## 泛型
>说明：泛型是对类型的限定，例如List<String>这样就只能传入字符串类型的数据，List<int>这样只能传入int类型的数据

**示例代码**

```
main() {
  //可以用var也行
  List<String> list = new List<String>();
  list.add('hello');
  list.add('world');

  //以下这行代码报错
  list.add(1);
  
  print(list);
}
```

**Map类型指定泛型的如下**

```
main() {
  var map = new Map<String, int>();
  map.addAll({'no':1});

  //以下这行代码报错
  map.addAll({'username':'zhangsan'});

  print(map);
}
```

### 修饰方法
>说明:修饰方法可以不对类型进行强制检查，能提高函数的复用性

**示例代码**

```

T returnValue<T>(T value) {
  return value;
}

main() {
  String name = returnValue('zhangsan');
  int age = returnValue(10);

  print('$name  $age');
}
```

**自定义List泛型输入**

```

class JSList<T> {
  var list = new List<T>();

  add(T value) {
    this.list.add(value);
  }
}

main() {
  var list = JSList<String>();
  list.add('helloworld');

  //以下这行代码报错，因为JSList限定了输入类型
  list.add(123);
}
```

### 泛型配合接口实现

```

abstract class A<T> {
  printInfo(T value);
}

class B<T> implements A<T> {
  @override
  printInfo(T value) {
    print('这是B的输出类型');
  }
}

class C<T> implements A<T> {
  @override
  printInfo(T value) {
    print('这是C的输出类型');
  }
}

main() {
  var b = new B<String>();
  var c = new C<int>();

  b.printInfo('hello world');
  c.printInfo(123);
}
```


