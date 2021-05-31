## 0 简介

**The Scala Programming Language**

Scala combines object-oriented and functional programming in one concise, high-level language. Scala's static types help avoid bugs in complex applications, and its JVM and JavaScript runtimes let you build high-performance systems with easy access to huge ecosystems of libraries.

- 面向对象
- 面向函数
- 静态类型   object
- 运行在JVM , 运行在脚本
- 可以访问现有的java的所有的类库

特点 

-   简洁 
-   优雅
-   快速 高效
-   灵活
-   有利于数据的流式处理 

scala底层就是java

spark底层是scala写的

## 1 环境

### 1.1 Windows上安装Scala编译器

- 官网下载 **xx.msi**，点击下一步即可
- 官网下载**xx.zip**,解压后，配置系统环境变量即可

### 1.2 Linux上安装Scala编译器

- 官网下载**xx.tgz**，解压后，配置系统环境变量即可

### 1.3 IDEA安装Scala编译器

- 下载Scala插件，然后重启IDEA即可

- 创建Scala项目

![IDEA创建Scala项目](E:\GitHubDemos\notes\scala\SCALA.assets\IDEA创建Scala项目.png)

## 2 运行

## 3 Scala基础知识

### 3.1 数据类型

![image-20210531145149531](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210531145149531.png)

- Any : 所有类型的父类 , 类似于java中的Object

- AnyVal: 数值类型(简单类型)

- AnyRef: 引用数据类型

- Null: 应用类型的子类,类似于java中的null ,是所有引用类型的子类

- Nothing: 所以类型的子类 可以返回给任意的变量或者函数 通常异常时使用,表示此处有错误

### 3.2 定义变量

- 格式：  var | val  变量名称:变量类型 = 变量值

- 数据类型可以省略 ,scala编译器可以对数据类型进行推断。

- var 可变的变量

- val 不可变的变量 (在不改变值的情况下优先使用val)

```scala
val name:String = "zss"	// 不可变的
var age = 10		// 可变的

// 变量可以批量设置(方法已经过时)
val (num1:Int, num2:String) = Pair(23, "zs")
```

### 3.3 运算符

- scala的运算符与java大致相同，但不同的是**scala中的运算符也是一种对象，有自己的方法**

### 3.4 流程控制

#### 3.4.1 if...else 语句

- if...else 语句与java一样，可以嵌套，可以有多个else...if

- **if...else 语句会返回一个值，因此可以将返回值赋给一个变量**

```scala
val x = 1
if(x>0){
    println("x > 0")
}else{
    println("x <= 0")
}

// 返回值赋给变量
val y = if(8>0) 1 else -1	// 类似于java中的三目运算符

val z = 0
// 将 if...else if...else 返回值赋给了result
val result = {
    if(z < 0)
    	1
    else if(z >= 1)
    	-1
    else
    	"error"
}
```

#### 3.4.2 while 循环 与do...while 循环

- while 循环、do...while 循环与java 中的使用方法完全相同
- **i++,i--不可以在Scala中使用，统一写为 i += 1, i -= 1**

```scala
// while 循环
var n = 10
while(n<20){
    println(n)
    n += 1	// 此处不可以使用n++,Scala中没有n++、n--方法
}

// do...while 循环
var m = 10
do{
    println("m:"+m)
    n -= 1
}while(m<10&&m>0)
```

#### 3.4.3 for 循环

- **for 循环**与java中的for循环区别很大，Scala中的for循环更为强大
- 常用语法

```scala
1. for(i <- 表达式)	// 表达式 1 to 10返回一个Range(区间)	
2. for(i <- 数组)		
3. for(i <- 1 to 3; j <- 1 to 2)	//嵌套for循环	(中间用 ; 隔开)
4. for(i <- 1 to 3; j <- 1 to 2 if i != j)		// 嵌套for循环再加上一个if作为过滤条件
5. val v = for(i <- 1 to 10) yield i
// 将for循环中满足条件的元素放入了v中	(yield 可以将结果输出到一个变量保存起来)
```

- 实例

```scala
// 遍历区间(Range)
	//to 可以替换为 until (until不包含右边的值，即为 1...9) 
for(i <- 1 to 10){
    println(i+"\t")	
}

// 遍历数组
val arr = Array(1,2,3)
for(i <- arr){
   println(i) 
}

// 嵌套for
for(i <- 1 to 3; j <- 1 to 3){
    println(i * j)
}

// 加条件的嵌套for
for(i <- 1 to 10; j <- 1 to 10; if i%2 == 0 && j%2 == 0){
    println(i * j)
}

// 将结果输出到一个变量中
val v = for(i <- 1 to 10) yield i * 10
```

#### 3.4.4 对循环的控制

- 使用方法

```scala
// 即将需要控制的语句块作为参数放在breakable后面，然后，其内部在某个条件满足时调用break方法，程序将跳出breakable方法。通过这种通用的方式，就可以实现Java循环中的break和continue功能。
breakable{
	...
	if(...) break
    ...
}
```

- 案例

```scala
var arr = Array(1,2,3)

// 相当于java中的break
breakable{
    for(i <- arr){
        if(i > 5) break	// 跳出breakable，结束循环
        println(i)
    }
}

// 相当于java中的continue
for(i <- arr){
    breakable{
        if(i > 5) break	// 跳出breakable，执行下一次循环
        println(i)
    }
}
```

#### 3.4.5 异常处理结构

- 和java一样的用法

```scal
try{
	...
}catch{
	...
}finally{
	...
}
```



### 3.5 数据结构

> scala中的集合分为两种 ,可变集合和不可变集合, 不可变集合可以安全的并发的访问!
>
> 集合的类主要在一下两个包中
>
> 1) 可变集合包  scala.collection.mutable
> 2) 不可变集合包 scala.collection.immutable（默认）
>
> scala默认使用的是不可变的集合 , 因此使用可变的集合需要导入可变集合的包
>
> scala的集合主要分成三大类
>
> (1) Seq 序列
>
> (2) Set 不重复集
>
> (3) Map 键值映射集
>
> 注意: 所有的集合都继承自Iterator迭代器这个特质

- Array(数组)	
- Tuple(元组)
- List(列表)
- Map(映射)
- Set(集合)
- Iterator(迭代器)

![scala数据结构](E:\GitHubDemos\notes\scala\SCALA.assets\scala数据结构.png)

#### 3.5.1 Array

```scala
// 整形数组
val arr = Array[Int](10,2,3)
// 通用数组
val arr2 = Array("JVM",12,flase)

// 取值(通过 (x) 的方法取值，x是索引，x从0开始)
arr(0)	//取出 10
```

#### 3.5.2 Tuple

```scala
// 定义Tuple
val tuple = (5,2,3)
val tuple1 = ("BigData",2015,45.0)

// 取值(通过 tuple._x 的形式取值，x为第几个位置，x从1开始)
tuple._1 	//取出 5
```

#### 3.5.3 List(重写了toString方法)

```scala
// 定义一个List
val ls = List[Int](1,2,3)
val ls2 = List(1,2.3,"Spark")
// 通过已有的List创建新的List
val ls3 = "Apache"::ls2	// ls2 不变，生成一个新的ls3
// 借助Nil(空列表对象)创建新的List
val ls4 = 1::2::3::Nil	// 等同于ls(Nil不可以省略)

// 取值(通过 (x) 的方法取值，x是索引，x从0开始)
ls(0)	// 取出1
```

#### 3.5.4 Map

```scala
// 定义Map
val mp = Map("zss" -> 1, "lss" -> 2)
val mp2 = Map(("zss",1),("lss",2))

// 取值(通过 mp(key) 来取得对应的value值)
mp("zss")	// 取出 1
```



#### 3.5.5 Set(元素不重复)

```scala
// 定义Set
val set = Set(1,2,3)
```

#### 3.5.6 Iterator

**只能按从前往后的顺序依次访问其元素**

```scala
// 定义Iterator
val iter = Iterator("Hadoop","Spark","Scala")
while (iter.hasNext) {
    println(iter.next())
}
```

## 4 面向对象编程基础

### 4.1 类

#### 4.1.1 类的定义

> 在类的定义中，字段和方法统称为类的成员（Member），其中，字段是指对象所包含的变量，它保存了对象的状态或者数据，而方法是使用这些数据对对象进行各种操作的可执行程序块。
>
> 字段的定义和变量的定义一样，用val或var关键字进行定义，方法用关键字def定义，基本的语法为：def 方法名(参数列表)：返回结果类型={方法体}

```scala
// Counter为类名
class Counter{
    // 这里定义类的字段和方法
}

// 完整的类的定义
class Counter{
    var value = 0	// 字段
    def increment(step:Int):Unit = {value += step}	// 方法一
    def current():Int = {value}	// 方法二
}

// 通过new实例化
val myCounter = new Counter
myCounter.value = 5	// 访问字段
println(myCounter.current)	// 调用方法
```

#### 4.1.2 类成员的可见性

> 在Scala类中，所有成员的默认可见性为公有，且不需要用public关键字进行限定，任何作用域内都能直接访问公有成员。除了默认的公有可见性，Scala 也提供与 Java 类似的可见性选项，包括private 和 protected，其中，private 成员只对本类型和嵌套类型可见；protected 成员对本类型和其继承类型都可见。

- 权限修饰符通用于主构造器，辅构造器，以及普通方法 

- private的具体用法

```scala
private 作用域为类和其伴生对象 
private [this] ，作用域为当前类中，伴生对象中无效 
private [packageName] 指定包及其子包有效 包名的写法，直接写包名，不需要层级路径 
```



#### 4.1.3 方法的定义方式

```scala
def functionName ([参数列表]) : [return type] = {
   function body
   return [expr]
}
// 没有等号和方法体的方法称为抽象方法,抽象方法定义在抽象类和特质中
```

#### 4.1.4 构造器

> 每个类都有一个**主构造器**，这个构造器和类定义"交织"在一起类名后面的内容就是主构造器，
> 如果参数列表为空的话，()可以省略
> scala的类有且仅有一个主构造器，要想提供更加丰富的构造器，就需要使用辅助构造器,辅助构造器是可选的，它们叫做**this**
>
> 注意：主构造器会执行类定义中的所有语句 

- 主构造器

```scala
// 有一个参数的主构造器，参数为name
class Counter(name:String){
    
}
```

- 辅助构造器

辅助构造器的名字**this**不可以改变，

每个辅助构造器的第一个表达式必须是调用一个此前已经定义的辅助构造器或主构造器，调用的形式为“this（参数列表）”

```scala
// 定义一个参数的辅助构造器,参数为age
def this(age:Int){
    this()	// 调用主构造器
}
```

### 4.2 对象

#### 4.2.1 单例对象

> 单例对象在第一次被访问的时候初始化。需要强调的是，定义单例对象不是定义类型，即不能实例化Person类型的变量，这也是被称为“单例”的原因。单例对象包括两种，即伴生对象（Companion Object）和孤立对象（Standalone Object）。当一个单例对象和它的同名类一起出现时，这时的单例对象被称为这个同名类的“伴生对象”。没有同名类的单例对象，被称为孤立对象

- 单例对象

```scala
object Person{
    val name = "zss"
}
```

- 伴生对象和伴生类

> 当单例对象与某个类具有相同的名称时，它被称为这个类的“伴生对象”（Companion Object），相应的类被称为这个单例对象的“伴生类”（Companion Class）。伴生对象和它的伴生类必须位于同一个文件中，它们之间可以相互访问对方的私有成员。

```scala
class Person(val name:String){
    private val id = Person.newPersonId()	// 调用了伴生对象的方法
    def info{
        printf("The id of %s is %d.\n",name,id)
    }
}

object Person{
    private var lastId = 0	
    def newPersonId()={
        lastId += 1
        lastId
    }
}
```

#### 4.2.2 apply方法

> ```scala
> val myStrArr = Array("BigData","Hadoop","Spark")
> ```
>
> 可以看到，这里并没有使用new关键字来创建Array对象。采用这种语法格式时，Scala会自动调用Array类的伴生对象Array中的一个称为apply的方法，来创建一个Array对象myStrArr。在Scala中，apply方法遵循如下的约定被调用：用括号传递给类实例或对象名一个或多个参数时，Scala会在相应的类或对象中查找方法名为apply且参数列表与传入的参数一致的方法，并用传入的参数来调用该apply方法。

#### 4.2.3 unapply方法

> unapply方法用于对对象进行解构操作，与apply方法类似，该方法也会被自动调用。可以认为unapply方法是apply方法的反向操作，apply方法接受构造参数变成对象，而unapply方法接受一个对象，从中提取值。unapply方法包含一个类型为伴生类的参数，返回的结果是Option类型（将在2.3.3节中介绍Option类型），对应的类型参数是N元组，N是伴生类中主构造器参数的个数。

### 4.3 继承

#### 4.3.1 抽象类

> 如果一个类包含没有实现的成员，则必须使用abstract关键词进行修饰，定义为抽象类。没有实现的成员是指没有初始化的字段或者没有实现的方法。

```scala
/*抽象类中的抽象字段必须要有声明类型。与Java不同的是，Scala里的抽象方法不需要加abstract修饰符。
抽象类不能进行实例化，只能作为父类被其他子类继承。
*/
abstract class Car(val name:String){
    val carBrand:String	// 字段没有初始值，就是一个抽象字段
    def info()	// 抽象方法
    def greeting(){
        println("Welcome to my car!")
    }
}
```

#### 4.3.2 类的继承

> 像Java一样，Scala只支持单一继承，而不支持多重继承，即子类只能有一个父类。在类定义中使用extends关键字表示继承关系。定义子类时，需要注意以下几个方面：
>
> 重载父类的抽象成员（包括字段和方法）时，override 关键字是可选的；而重载父类的非抽象成员时，override关键字是必选的

#### 4.3.3 Option类

> 类Option是一个抽象类，有一个具体的子类Some和一个对象None，其中，前者表示有值的情形，后者表示没有值。在Scala的类库中经常看到返回Option[T]的方法，其中，T为类型参数。对于这类方法，如果确实有T类型的对象需要返回，会将该对象包装成一个Some对象并返回；如果没有值需要返回，将返回None。

#### 4.3.4 参数化类型

> 与Java及C++中的泛型类似，Scala支持参数化类型。所谓参数化类型，是指在类的定义中包含一个或几个未确定的类型参数信息，其具体的类型将在实例化类时确定。Scala使用方括号（[…]）来定义参数化类型。

- 实例

```scala
// 下面的脚本通过对Scala中的栈类型Stack进行简单地封装，定义了一个参数化类型Box。
class Box[T]{
    val elem:Stack[T] = Stack()
    def remove:Option[T]={
        // 返回的对象采用了Option类型进行包装
        if(elem.isEmpty)	None
        else	Some(elems.pop)
    }
    def append(a1:T){
        elem.push(a1)
    }
}
// 上例中的T属于类型信息，在实例化Box类时需要给T赋值具体的类型。
```

#### 4.3.5 Trait(特质)

> 类似于java中的接口。
>
> Scala的特质是代码重用的基本单元，可以同时拥有抽象方法和具体方法。Scala中，一个类只能继承自一个超类，却可以混入（Mixin）多个特质，从而重用特质中的方法和字段，实现了多重继承。

```scala
// 定义特质
trait Flyable{
    var maxFlyHeight:Int	// 抽象字段
    def fly()	// 抽象方法
    def breathe(){
        // 具体的方法
        println("I can breathe")
    }	
}
```

特质可以使用extends继承其他的特质，并且还可以继承类。

```scala
trait T1{
    def move()
}
trait T2 extends T1{
    def fly()
    def move(){
        println("I move by flying.")	//重载了父特质的抽象方法
    }
}
```

特质定义好以后，就可以使用extends 或with 关键字，把它混入到类中。当把特质混入类中时，如果特质中包含抽象成员，则该类必须为这些抽象成员提供具体实现，除非该类被定义为抽象类。

```scala
class Bird(flyHeight:Int) extends Flyable{
    // 重载特质的抽象字段
    var maxFlyHeight:Int = flyHeight	
    // 重载特质的抽象方法
    def fly(){
        printf("I can fly at the height of %d.",maxFlyHeight)
    }
}
```

如果要混入多个特质，可以连续使用多个 with。

```scala
trait Flyable{
    var maxFlyHeight:Int	// 抽象字段
    def fly()	// 抽象方法
    def breathe(){
        // 具体的方法
        println("I can breathe")
    }	
}

trait HasLegs{
    val legs:Int	// 抽象字段
    def move(){printf("I can walk with %d legs",legs)}
}

class Animal(val category:String){
    def info(){println("This is a " + category)}
}

class Bird(flyHeight:Int) extends Animal("Bird") with Flyable with HasLegs{
    var maxFlyHeight:Int = flyHeight
    val legs = 2
    def fly(){
        printf("I can fly at the height of %d",maxFlyHeight)
    }
}
```

除了可以在类的定义中混入特质，还可以在实例化某一类型时直接混入特质，这时只能用 with关键字，而不能用extends

```scala
class Animal(val category:String){
    def info(){println("This is a "+category)}
}

trait HasLegs{
    val legs:Int
    def move(){prinf("I can walk with %d legs",legs)}
}

object Test{
    def main(args:Array[String]):Unit={
        var a = new Animal("dog") with HasLegs{
            val legs = 4	// 抽象特质的抽象字段
        }
    }
}
```

### 4.4 模式匹配

#### 4.4.1 match 语句

最常见的模式匹配是match语句，match语句用在当需要从多个分支中进行选择的场景，类似于Java中的switch语句。可以匹配以下几种：

- 字符串
- 数据类型
- 元组
- List 和 Array
- 样例类和样例对象
- Option

```scala
// 例子一
for (elem <- List(6,9,0.618,"Spark","Hadoop",'Hello)){
    val str = elem match {
        case i: Int => i + " is an int value."		// 匹配整型的值，并赋值给i　　　　
        case d: Double => d + " is a double value." // 匹配浮点型的值　　　　
        case "Spark"=>"Spark is found." 			// 匹配特定的字符串
        case s: String => s + " is a string value." // 匹配其他字符串　　　　
        case _ =>"unexpected value:"+ elem 			// 与以上都不匹配　　
    }
}

// 例子二
for (elem <- List(1,2,3,4)){
    elem match {
        case _ if (elem%2==0) => println(elem + "is even.")　　　　　// 匹配条件符合的情况
        case _ => println(elem + " is odd.")　　
    }
}
```

#### 4.4.2 case类(样例类)

> 当定义一个类时，如果在class关键字前加上case关键字，则该类称为case类。
>
> Scala为case类自动重载了许多实用的方法，包括toString、equals和hashcode方法，其中，toString会返回形如“类名（参数值列表）”的字符串。
>
> 更重要的是，Scala为每一个case类自动生成一个伴生对象，在该伴生对象中自动生成的模板代码包括：
>
> - 一个apply方法，因此，实例化该类的时候无需使用new关键字；
> - 一个unapply方法，该方法包含一个类型为伴生类的参数，返回的结果是Option类型，对应的类型参数是N元组，N是伴生类中主构造器参数的个数。Unapply方法用于对对象进行解构操作，在case类模式匹配中，该方法被自动调用，并将待匹配的对象作为参数传递给它。

对case类而言，最常见的使用场景就是模式匹配，

```scala
case class Car(brand: String, price: Int)	// case 类

val myBYDCar = new Car("BYD", 89000)　　
val myBMWCar = new Car("BMW", 1200000)　　
val myBenzCar = new Car("Benz", 1500000)　　
for (car <- List(myBYDCar, myBMWCar,myBenzCar)) {
    car match{
        case Car("BYD", 89000) => println("Hello,BYD!")　　　
        case Car("BMW", 1200000) => println("Hello,BMW!")　　　
        case Car(brand, price) => println("Brand:"+brand +", Price:"+price+", do you want it?")
    }
}
// 上例中每一个case子句中的Car(…)，都会自动调用Car.unapply(car)，并将提取到的值与Car后面括号里的参数进行一一匹配比较，对于第一个case和第二个case是与特定的值进行匹配，第三个case由于Car后面跟的参数是变量，因此将匹配任意的参数值。
```

对case类而言，除了可以在match表达式中进行模式匹配，还可以在定义变量时直接从对象中提取属性值。

```scala
val myBYDCar = new Car("BYD", 89000)　

val Car(brand,price)=myBYDCar	// 调用unapply 方法，返回brand和price属性
```

### 4.5 包

- 与Java不同的是，Scala的包和源文件之间并没有强制的一致层次关联关系

- 把代码放在包里的另一种方式是在 package 子句之后加一对大括号，再将相关的类及对象放到大括号里。这种语法的好处是可以将程序的不同部分放在不同的包里。
- Scala 的包定义支持嵌套，相应的作用域也是嵌套的，在包内可以直接访问其父级包内定义的内容。
- 包和其成员可以用import 子句来引用，这样可以简化包成员的访问方式。
- 类似于Java的通配符*,Scala使用通配符下划线（_）引入类或对象的所有成员（*是合法的Scala标识符）
- 与Java不同的是，Scala的import语句并不一定要写在文件顶部，它可以出现在程序的任何地方，其作用域从 import语句开始一直延伸到包含该语句的块的末尾，该特性在大量使用通配符引入时显得尤为重要，可以很好地避免命名冲突。

```scala
// xmu 包里面有两个包：autodepartment 和 csdepartment
package xmu {　
    package autodepartment {　　
        class ControlCourse{　　　　...　　}　
    }
    // 可以直接访问大包内的成员：另一个包的类
    package csdepartment {　　
    class OSCourse{　　val cc = new autodepartment.ControlCourse　　}　
	}
}

// 使用import引用包及其成员
import xmu.autodepartment.ControlCourse
class MyClass{
    var myos = new ControlCourse
}

// 使用import导入整个包的内容
import scala.io.StdIn._
var i=readInt()
var f=readFloat()
var str=readLine()
```

## 5 函数式编程基础

> Scala在架构层面上提倡上层采用面向对象编程，而底层采用函数式编程。Scala不是完全的函数式编程语言，也不要求变量不可变，但它推荐尽量采用函数式来实现具体的算法和操作数据，多用val，少用var。这种做法不仅可以大大减少代码的长度，还可以降低出错的概率

### 5.1 函数的定义与使用

> 定义函数最通用的方法是作为某个类或者对象的成员，这种函数被称为方法，其定义的基本语法为“def 方法名（参数列表）：结果类型={方法体}”
>
> ```scala
> val| var 函数名称=（函数的参数列表） => 函数体
> ```

```scala
val counter:(Int) => Int ={
    value = value + 1
}
val counter = (value:Int) => value + 1	// 匿名函数

```

### 5.2 高阶函数

> 当一个函数包含其他函数作为其参数或者返回结果为一个函数时，该函数被称为高阶函数。
>
> 可以说，支持高阶函数是函数式编程最基本的要求，高阶函数可以将灵活、细粒度的代码块集合成更大、更复杂的程序。

```scala
def sum(f: Int => Int, a: Int, b: Int):Int = {　　
    if(a > b) 0 
    else f(a) + sum(f, a+1, b)
}
// 现在不同的求和都统一调用方法sum，只需要为函数参数f传入不同的函数值
scala> sum(x=>x,1,5) // 直接传入一个匿名函数
res8: Int = 15

scala> sum(x=>x*x,1,5) // 直接传入另一个匿名函数
res9: Int = 55

scala> sum(powerOfTwo,1,5) //传入一个已经定义好的方法
res10: Int = 62
```

### 5.3 闭包

> 当函数的执行依赖于声明在函数外部的一个或多个变量时，则称这个函数为闭包。

闭包可以捕获闭包之外对自由变量的变化

```scala
scala> var more = 10
more: Int = 10
scala> val addMore =(x:Int)=> x + more	// 调用了函数外面声明的变量 more
addMore: Int => Int = <function1>
scala> addMore(5) // more的值被绑定为10
res7: Int = 15
scala> more=20
more: Int = 20
scala> addMore(5)// more的值被绑定为20
res8: Int = 25
```

反过来，闭包对捕获变量做出的改变在闭包之外也可见。

```scala
scala> var sum=0
sum: Int = 0
scala> val accumulator = (x:Int)=>sum+=x // 包含外部变量sum的闭包
accumulator: Int => Unit = <function1>
scala> accumulator(5)
scala> sum
res13: Int = 5
scala> accumulator(10)
scala> sum
res15: Int = 15
```



### 5.4 偏应用函数和Curry化

#### 5.4.1 偏应用函数

```scala
/*这里的sum是一个带有3个参数的函数，函数变量a是用sum来定义的，并将sum的第一个参数确定为1，而剩下的两个参数用下划线（_）表示，相当于只保留了sum的部分参数。这种只保留了函数部分参数的函数表达式，称为偏应用函数（Partially Applied Function）。
*/
def sum(a:Int,b:Int,c:Int) = a + b + c
val a = sum(1,_:Int,_:Int)	// 只保留了sum的后两个参数
val b = sum _	// 保留了sum的全部参数
val res:Int = a(2,3)
val res2:Int = b(1,2,3)
```



#### 5.4.2 Curry 化

Curry化的函数是指那种带有多个参数列表且每个参数列表只包含一个参数的函数。

```scala
scala> def multiplier(factor:Int)(x:Int)=x*factor
multiplier: (factor: Int)(x: Int)Int // 带有两个参数列表的函数
scala> val byTwo=multiplier(2)_  // 保留multiplier第二个参数的偏应用函数，第一个参数值固定为2
scala> multiplier(2)(5)
res2: Int = 10
scala> byTwo(5)
res3: Int = 10
// 这里的multiplier函数也称为Curry化的函数。随后第2条语句采用偏应用函数的形式转化成了只带有一个参数的函数byTwo。
```

可以通过Curry化过程，将一个多参数的普通函数转化为Curry化的函数

```scala
scala> def plainMultiplier(x:Int,y:Int)=x*y
plainMultiplier: (x: Int, y: Int)Int // 带有两个参数的普通函数
scala> val curriedMultiplier = (plainMultiplier_).curried
curriedMultiplier: Int => (Int => Int) = <function1>
scala> plainMultiplier(2,5)
res5: Int = 10
scala> curriedMultiplier(2)(5)
res6: Int = 10
```

### 5.5 针对容器的操作

#### 5.5.1 遍历操作

- Scala容器的标准遍历方法为foreach方法，该方法的原型为：

  ```scala
  // 语法
  def foreach[U](f: Elem => U) :Unit
  
  // 实例
  var ls = List(1,2,3)
  ls foreach println	// 中缀表示法
  val mp = Map("zs" -> 1, "ls" -> 2)
  mp foreach println
  ```

  - for遍历

  ```scala
  val ls = List(1,2,3)
  for(i <- ls)
  println(i)
  
  val mp = Map("zs" -> 1, "ls" -> 2)
  for(kv <- mp) println(kv._1+":"+kv._2)
  println(k+":"+v)	// 与上一句的效果一样
  ```

#### 5.5.2 映射操作

映射是指通过对容器中的元素进行某些运算来生成一个新的容器。

- map 方法

```scala
/*map方法将某个函数应用到集合中的每个元素，映射得到一个新的元素，因此，map 方法会返回一个与原容器类型大小都相同的新容器，只不过元素的类型可能不同*/
val books = List("Hadoop","Hive","HDFS")
books.map(s => s.toUpperCase) // 将一个字符串的每个字母都变成大写字母
books.map(s => s.length)	// 将字符串映射到它的长度
```

- flatMap方法

```scala
/*flatMap方法稍有不同，它将某个函数应用到容器中的元素时，对每个元素都会返回一个容器（而不是一个元素），然后，flatMap把生成的多个容器“拍扁”成为一个容器并返回。返回的容器与原容器类型相同，但大小可能不同，其中元素的类型也可能不同。*/
scala> books flatMap (s => s.toList)
res58: List[Char] = List(H, a, d, o, o, p, H, i, v, e, H, D, F,S)	// flatMap 将各个字符串返回的List[Char]“拍扁”成一个List[Char]。
```

#### 5.5.3 过滤操作

- filter

```scala
scala> val l=List(1,2,3,4,5,6) filter {_%2==0}	// 使用了占位符语法，过滤出能被2整除的元素
```

- filterNot

```scala
scala> val l=List(1,2,3,4,5,6) filterNot {_%2!=0}	// 使用了占位符语法，过滤掉不能被2整除的元素
```

- 与过滤操作相关的几个常用函数还包括exists和find，其中，exists方法判断是否存在满足给定条件的元素，find方法返回第一个满足条件的元素

```scala
scala> val t=List("Spark","Hadoop","Hbase")
t: List[String] = List(Spark, Hadoop, Hbase)
scala> t exists {_ startsWith "H"} // startsWith为String的函数
res3: Boolean = true
scala> t find {_ startsWith "Hb"}
res4: Option[String] = Some(Hbase) // find的返回值用Option类进行了包装
scala> t find {_ startsWith "Hp"}
res5: Option[String] = None
```

#### 5.5.4 规约操作

> 规约操作是对容器的元素进行两两运算，将其“规约”为一个值。最常见的规约方法是 reduce方法，它接受一个二元函数f作为参数，首先将f作用在某两个元素上并返回一个值，然后再将f作用在上一个返回值和容器的下一个元素上，再返回一个值，依此类推，最后容器中的所有值会被规约为一个值。

- reduce 方法

```scala
scala> val list =List(1,2,3,4,5)
list: List[Int] = List(1, 2, 3, 4, 5)
scala> list.reduce(_ + _) // 将列表元素累加，使用了占位符语法
res16: Int = 15
scala> list.reduce(_ * _) // 将列表元素连乘
res17: Int = 120
scala> list map (_.toString) reduce ((x,y)=>s"f($x,$y)")
res5: String = f(f(f(f(1,2),3),4),5) // f表示传入reduce的二元函数
```

> reduce方法对元素进行操作时，对于List等有序容器而言（即容器中的元素有顺序关系），其遍历容器的默认顺序是从左到右，而对于Set等无序容器而言（即容器中的元素没有顺序关系），其遍历容器的顺序是未定的，因此，其结果对于无序容器而言可能是不确定的
>
> 为了保证遍历顺序，有两个与reduce相关的方法，reduceLeft和reduceRight，从名字即可看出，前者从左到右进行遍历，后者从右到左进行遍历。reduceLeft 和reduceRight 对传入的二元函数的参数定义不相同，对于reduceLeft，第一个参数表示累计值，对于reduceRight，第二个参数表示累计值。

- fold 方法(Curry 化的函数)

> fold方法是一个双参数列表的函数，第一个参数列表接受一个规约的初始值，第二个参数列表接受与reduce中一样的二元函数参数。两个方法唯一的差别是， reduce是从容器的两个元素开始规约，而fold则是从提供的初始值开始规约。同样地，对于无序容器而言， fold方法不保证规约时的遍历顺序，如要保证顺序，请使用foldLeft和foldRight，其中，关于匿名函数参数的定义，与reduceLeft和reduceRight完全一样。
>

```scala
scala> val list =List(1,2,3,4,5)
list: List[Int] = List(1, 2, 3, 4, 5)
scala> list.fold(10)(_*_)
res32: Int = 1200
scala> (list fold 10)(_*_) // fold的中缀调用写法
res33: Int = 1200
scala> (list foldLeft 10)(_-_) // 计算顺序(((((10-1)-2)-3)-4)-5)
res34: Int = -5
scala> (list foldRight 10)(_-_) // 计算顺序(1-(2-(3-(4-(5-10)))))
res35: Int = -7
scala> val em = List.empty
em: List[Nothing] = List()
scala> em.fold(10)(_-_)// 对空容器fold的结果为初始值，对空容器调用reduce会报错
res36: Int = 10
```

reduce操作总是返回与容器元素相同类型的结果，但是，fold操作可以输出与容器元素类型完全不同类型的值，甚至是一个新的容器。

#### 5.5.5 拆分操作

> 拆分操作是把一个容器里的元素按一定的规则分割成多个子容器。常用的拆分方法有partition、groupedBy、grouped和sliding。

```scala
// 假设原容器为C[T]类型。
// partition方法接受一个布尔函数，用该函数对容器元素进行遍历，以二元组的形式返回满足条件和不满足条件的两个 C[T]类型的集合。
// groupedBy方法接受一个返回U类型的函数，用该函数对容器元素进行遍历，将返回值相同的元素作为一个子容器，并与该相同的值构成一个键值对，最后返回的是一个类型为 Map[U,C[T]]的映射。
// grouped和sliding方法都接受一个整型参数n，两个方法都将容器拆分为多个与原容器类型相同的子容器，并返回由这些子容器构成的迭代器，即Iterator[C[T]]。其中，grouped按从左到右的方式将容器划分为多个大小为n的子容器（最后一个的大小可能小于n）;
// sliding使用一个长度为n的滑动窗口，从左到右将容器截取为多个大小为n的子容器。
```

```scala
val xs = List(1,2,3,4,5)
val part = xs.partition(_<3)	// 分为小于3 的和不小于3的， 返回两个结果
val gby = xs.groupBy(x => x%3)	// 按被3整除的余数进行划分， 返回xs.length % 3份结果
val ged = xs.grouped(3)	// 拆分为3个子容器
val sli = xs.slice(0,2)	// 返回从0到2的元素，下标从0开始
val sl = xs.sliding(2,2)	// 将列表按照固定大小2进行分组，步进为2，步进默认为1，返回结果为迭代器
```



