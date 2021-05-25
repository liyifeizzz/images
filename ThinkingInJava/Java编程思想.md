# Java编程思想

## 一切都是对象

### 1.用引用操作对象

在Java中所有的一些都被视为对象,尽管一切都被视为了对象,但操作的标识符实际上是一个"引用".

```java
class Person{
    String name;
    int age;
}

public class OnePointOne {
    public static void main(String[] args) {
        Person person;
    }
}
```

由上面的例子可以知道,创建一个**Person**的引用Person person,但这里**创建的只是引用而不是对象**,创建一个安全的对象引用是要将对象引用进行初始化.

### 2.必须由你创建所有对象

一旦创建了一个对象引用,就希望它能与一个新的对象相关联.通常用**new**操作符实现这个目的.

```Java
class Person{
    String name;
    int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class OnePointOne {
    public static void main(String[] args) {
        Person person;              // 对象引用
        person = new Person();      // 对象
    }
}
```

由上可以知道,Person person 是创建了Person对象的引用,而person = new Perosn() 创建这个对象,还有另外的一种写法Person person = new Person();

***2.1特例:不需要new来创建对象--基本类型***

| 基本类型 | 大小  | 包装类型  |
| -------- | ----- | --------- |
| boolean  | -     | Boolean   |
| char     | 2字节 | Character |
| byte     | 1字节 | Byte      |
| short    | 2字节 | Short     |
| int      | 4字节 | Integer   |
| long     | 8字节 | Long      |
| float    | 4字节 | Float     |
| double   | 8字节 | Double    |
| void     | -     | Void      |

### 3.永远不需要销毁对象

**3.1作用域**

大多数过程语言都有作用域的概念,作用域决定了其内定义变量名的可见性和生命周期.在Java中,作用域由花括号的位置决定.

```Java
public class TwoPointOne {
    int x = 0;

    public void test(){
        int y = 1;
        y = x;
    }
}
```

由上可知,x的作用域位于TwoPointOne{}中,y的作用域位于test(){}中,z所以x的作用域>y的作用域.

**3.2对象的作用域**

Java对象不具备和基本类型一样的生命周期.当用new 创建一个Java对象之后,它可以存活于作用域之外.

```Java
public void test2(){
        String s  = new String("123");
    }
```

根据上可知,引用s在作用域终点消失了.然而,s指向的String 对象仍继续占据内存单元,但是我们无法在这个作用域之后访问这个对象.

### 4.创建新的数据类型:类

**class**关键字用来创建新的数据类型,比如创建Person数据类型class Person{ }

**4.1字段和方法**

一旦定义了一个类,就可以在类中设置两种类型的元素:**字段和方法.**

**字段**可以是任何类型的数据,可以通过其引用与其通信;也可以是基本类型的一种,如果字段是某个对象的引用,那么必须初始化该引用,以便使其与一个实际对象相关联(使用new来实现).

```Java
// 女朋友类
class GirlFriend{
    String name; // 姓名
   int height;  // 身高
   int weight;  // 体重
}


// Person类型
class Persons{
    String name;            // 姓名
    GirlFriend girlFriend  = new GirlFriend();  // 女友
}
```

由上面可见,GirlFriend类的字段有name,height,weight;Persons类的字段有name , girlFriend;

可以通过引用进行字段赋值

```java 
		Persons persons = new Persons();
        persons.name = "123";
        persons.girlFriend.name = "321";
        persons.girlFriend.height = 165;
        persons.girlFriend.weight = 50;
```

这样就可以将Persons类的字段全部进行赋值,同理GirlFriend也可以进行赋值.

**方法**在Java中表示为"做某些事情",其他的语言中运用函数来表示.方法的基本组成部分包括:名称,参数,返回值和方法体.

```Java
public void test(int i , int j){
        int k = i + j;
    }
    
    public int test(int i){
        return i*i;
    }
```

从上可知,有两个方法,这两个方法的名称都是test,第一个test的参数为i,j,第二个test的参数为j,第一个test返回值为void,第一个test的返回值为int,方法体为{}中的内容.

### 5.构建第一个Java程序

**5.1名字的可见**

为了给一个库生成不会与其它名字混淆的名字,Java设计者希望程序员反过来使用自己的域名,因为可以保证它们一定是唯一的

**5.2运用其他构建**

通过import关键字来准确告诉编译器你想要的类是什么.import指示编译器导入一个包.

比如:import java.util.List;

**5.3 static关键字**

当声明一个事物是**static**时,就意味着这个域或者方法不会与包含它的那个类的任何对象实例关联在一起.

只须将**static** 关键字放在定义之前,就可以将字段或方法设置为**static**.而且static字段对于一个类来说只有一份存储空间.

静态变量的引用,方法一:创建一个对象进行引用;方法二:通过类目引用.

静态方法的引用,方法一:创建一个对象进行引用;方法二:通过类目引用.

```Java
class Test{
    static int i = 1;   // 静态字段

    public static int test(){   // 静态方法
        return i;
    }
}

public class FourPointThree {
    public static void main(String[] args) {
        Test test = new Test();
        int j = test.i;        // 静态变量的引用方法一
        int k = Test.i;        // 静态变量的引用方法二
        test.test();           // 静态方法的引用方法一
        Test.test();           // 静态方法的引用方法二
    }
}
```

### 6.注释

注释分为三种:单行注释,多行注释,文档注释

```java 
/**
     * 测试方法(文档注释)
     * @param k:变量k
     */
    public void test1(int k){
        /*进行测试(多行注释)*/
        int i , j;  // 变量i,j(单行注释)
    }
```



## 操作符

### 1.赋值

赋值使用运算符"=",意思是"取右边的值,把它赋值给左边".

**1.1对基本类型的赋值**

```java
int i = 1;
String s = "abc";
```

**1.2对对象的赋值**

在对对象进行赋值时,我们真正操作是对对象的引用.所以,"将一个赋值给另一个对象",实际上是将"引用"从一个地方赋值到另一个地方.

```Java
class Number{
    int num;
}
public class OnePointOne {
    public static void main(String[] args) {
        Number number1 = new Number();
        Number number2 = new Number();
        number1.num = 10;   // 设置值
        number2.num = 20;
        System.out.println("number1="+number1.num+"  number2="+number2.num);
        number1 = number2;  // 赋值
        System.out.println("number1="+number1.num+"  number2="+number2.num);
        number2.num = 30;  // 修改值
        System.out.println("number1="+number1.num+"  number2="+number2.num);
    }
}
```

运行的结果为:![image-20210505213144465](C:\Users\Newbie\AppData\Roaming\Typora\typora-user-images\image-20210505213144465.png)

从上面的例子中,可以看出当我们修改了number2的值时,number1的值也会随之修改.从这里我们也可以得出,在进行对象的赋值时,number1,number2指向的都是相同的引用,它们指向相同的对象.

这种现象通常被称为"别名现象",是Java操作对象的一种基本方式.

那么如何避免出现别名现象?将程序的赋值操作进行如下修改:

```Java
class Number{
    int num;
}
public class OnePointOne {
    public static void main(String[] args) {
        Number number1 = new Number();
        Number number2 = new Number();
        number1.num = 10;   // 设置值
        number2.num = 20;
        System.out.println("number1="+number1.num+"  number2="+number2.num);
        number1.num = number2.num;  // 赋值
        System.out.println("number1="+number1.num+"  number2="+number2.num);
        number2.num = 30;  // 修改值
        System.out.println("number1="+number1.num+"  number2="+number2.num);
    }
}
```

运行结果为:![image-20210505213735122](C:\Users\Newbie\AppData\Roaming\Typora\typora-user-images\image-20210505213735122.png)

可见,只要将赋值操作修改为number1.num = number2.num,即可避免出现别名现象.

### 2.算术操作符

Java的算术操作符包括加号(+),减号(-),除号(/),乘号(*)以及取模运算(%)

```java
public class TwoPointOne {
    public static void main(String[] args) {
        int x = 3;
        int y = 4;
        // 加法
        System.out.println("x+y="+(x+y));
        // 减法
        System.out.println("x-y="+(x-y));
        // 乘法
        System.out.println("x*y="+(x*y));
        // 除法
        System.out.println("x/y="+(x/y));
        // 取模
        System.out.println("x%y="+(x%y));
    }

}
```

运算结果:![image-20210505214605560](C:\Users\Newbie\AppData\Roaming\Typora\typora-user-images\image-20210505214605560.png)

### 3.自动递增和递减

递减操作符 :--

递增操作符:++

令 int a;则a++可以看作为a=a+1;a--可以看作a=a-1

这两个操作符各有两种使用方式,通常称为"前缀式"和"后缀式",前缀递增(++a),前缀递减(--a),后缀递增(a++),后缀递减(a--).

**对于前缀式,会先执行运算,在生成值;对于后缀式,会先生成值,在执行运算**

```java
public class ThirdPointOne {
    public static void main(String[] args) {
        int a = 1;
        int b = ++a;
        System.out.println("a = "+a+" b = "+b);

        a = 1;
        b = a++;
        System.out.println("a = "+a+" b = "+b);
    }
}
```

结果为:![image-20210505215838313](C:\Users\Newbie\AppData\Roaming\Typora\typora-user-images\image-20210505215838313.png)

可见前缀式: int b = ++a;可拆分为 a = a +1 ; int b = a.后缀式 b = a++;拆分为b = a; a= a+1

### 4.关系操作符

关系操作符的结果是一个boolean结果,它们计算的是操作数值之间的关系.如果值之间的关系是真的,关系表达式会生成true,反之生成false.

关系操作符包括大于(>),小于(<),大于等于(>=),小于等于(<=),等于(==),不等于(!=)

**4.1基本操作符的等价性**

```java
public class FourPointOne {
    public static void main(String[] args) {
        // 1. 基本类型的等价性
        int x = 1;
        int y = 1;
        System.out.println(x == y);
        System.out.println(x != y);
    }
}
```

结果为:![image-20210506211748790](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210506211748790.png)

可见可以通过==和!=判断基本类型的等价性.那么对象的等价性是否能通过这种方法来验证呢?

**4.2对象的等价性**

```java
public class FourPointOne {
    public static void main(String[] args) {
        // 2.对象的等价性
        Integer integer1 = new Integer(1);
        Integer integer2 = new Integer(1);
        System.out.println(integer1 == integer2);
    }
}
```

结果为:![image-20210506212218868](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210506212218868.png)

由上面的结果可以知道,输出的是false,这跟我们所预想的结果是不一样的.那什么造成了输出的是false呢?两个Integer对象都是相同的,尽管对象的内容是相同的,但是对象的引用却是不同的,因为**==和!=比较的是对象的引用**.

为了避免上面情况的出现,我们要使用equals()方法来进行对象等价性的验证.

```java
public class FourPointOne {
    public static void main(String[] args) {
        // 2.对象的等价性
        Integer integer1 = new Integer(1);
        Integer integer2 = new Integer(1);
        System.out.println(integer1.equals(integer2));
    }
}
```

结果为:![image-20210506212959617](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210506212959617.png)

但当我们创建自己的类时,要覆盖equals()方法,才能进行对象的等价性验证.

### 5.逻辑操作符

逻辑操作符包括"与"(&&),"或"(||),"非"(!)能根据参数的逻辑关系,生成一个布尔值.

```java
public class FivePointOne {
    public static void main(String[] args) {
        int i = 1;
        int j = 2;
        System.out.println((i < 2) && (j > 2));
        System.out.println((i < 2) || (j > 2));
        System.out.println(!(i < 2));
    }
}
```

结果是:![image-20210506213855765](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210506213855765.png)

### 6.按位操作符

按位操作符用来操作整数基本数据类型中的单个"比特",即二进制位

按位操作符包括:位与(&),位或(|),异或(^),位非(~)

**6.1位与(&)**

对于两个二进制数,每位数按照"与"的逻辑,即同为1结果才为1,否则结果为0

```java
public class SixPointOne {

    public static void main(String[] args) {
        // 1.位于(&)
        // 5:0000 0000 0000 0101
        // 4:0000 0000 0000 0100
        // 5&4:0000 0000 0000 0100
        short i = 5;
        short j = 4;
        System.out.println(i&j);
    }
}
```

结果为:![image-20210507222833706](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210507222833706.png)

从上面的例子可以看出,5的二进制位0000 0000 0000 0101,4的二进制0000 0000 0000 0100,按照每位进行与运算,得到:0000 0000 0000 0100(4).

**6.2位或(|)**

对于两个二进制数,每位数按照"或"的逻辑,即只要一位为1结果就为1,否则结果为0

```java
public class SixPointOne {

    public static void main(String[] args) {
        short i = 5;
        short j = 4;

        // 2.位或(|)
        // 5:0000 0000 0000 0101
        // 4:0000 0000 0000 0100
        // 5|4:0000 0000 0000 0101
        System.out.println(i|j);
    }
}
```

结果为:![image-20210507223357352](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210507223357352.png)

从上面的例子可以看出,每位数按照"或"逻辑进行运算.

**6.3异或(^)**

对于两个二进制数,每位数按照"异或"的逻辑进行运算,即两位数的相异结果为1,相同结果为0(0⊕0=0,0⊕1=1,1⊕0=1,1⊕1=0)

```java
public class SixPointOne {

    public static void main(String[] args) {
        // 3.异或(^)
        // 5:0000 0000 0000 0101
        // 4:0000 0000 0000 0100
        // 5^4:0000 0000 0000 0001
        System.out.println(i^j);
    }
}
```

结果是:![image-20210507224007924](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210507224007924.png)

从上面的例子可以看出,每位数按照"异或"逻辑进行运算.

**6.4位非(~)**

位非是一个一元运算符,即将每位数都取反.

```java
public class SixPointOne {

    public static void main(String[] args) {
        // 4.位非(~)
        // 5:0000 0000 0000 0101
        // ~5:1111 1111 1111 1010
        System.out.println(Integer.toBinaryString(~5));
    }
}
```

结果为:![image-20210507224803826](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210507224803826.png)

从上面的例子可以看出,每位数按照"非"逻辑进行运算.

综上所述:所有的位运算只是对二进制的每位数进行运算.

### 7.移位操作符

移位操作符只可以用来处理整数类型.

**7.1左移位操作符<<**

比如 value << 1:表示将二进制的位数向左左移一位,符号位移除并舍弃,移动后的空位用"0"来填充.

```java
public class SevenPointOne {
    public static void main(String[] args) {
        // 1.左移
        int i = 5;
        System.out.println(Integer.toBinaryString(i));
        int j = i <<1;
        System.out.println(Integer.toBinaryString(j));
    }
}
```

结果为:![image-20210508232258579](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210508232258579.png)

由上面的例子可以看出,5的二进制为00000000 00000000 00000000 00000101

但5进行左移一位时,00000000 00000000 00000000 00001010

对于移位可能将这个数移位成一个负数的情况.也就是意味这将5移位29位将会变成负数,此时的二进制为:10100000 00000000 00000000 00000000.

**7.2右移位操作符>>**

比如 value >> 1:表示将二进制的位数向移右右移一位,末位移出并舍弃,左边加上符号位,如果是正数,符号位补0,如果是负数,符号位补1.

```Java
public class SevenPointOne {
    public static void main(String[] args) {
        // 2.右移
        int k = -5;
        System.out.println(Integer.toBinaryString(k));
        int m = k>>1;
        System.out.println(Integer.toBinaryString(m));
    }
}
```

结果是:![image-20210508233702792](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210508233702792.png)

**7.3无符号右移操作符>>>**

比如 value >> 1:表示将二进制的位数向移右右移一位,末位移出并舍弃,左边加上符号位,无论是正数还是负数,符号位补0.

无符号右移跟右移操作符类似,只是补位不同而已.

**补充:**

当int类型进行移位时的位数超过32位,会**先求余之后在进行移位**.即意味这要移位40位,先要40%32=8,所以移位8位.

当byte,char,short类型进行移位时,那么在移位之前,它们会被转换成int类型,并且得到的结果也是一个int类型.

当long类型进行移位时的位数超过64位,会**先求余之后在进行移位**.即意味这要移位70位,先要70%64=6,所以移位6位.

### 8.三元操作符

三元运算符采取下述的形式:boolean-exp ? value0 : value1

当boolean-exp的结果为true是,就计算value0.当boolean-exp的结果为false,就计算value1.

```java
public class EightPointOne {
    public static void main(String[] args) {
        int a = 3;
        int b = 2;
        int c = (a > b) ? a + b : a - b;
        System.out.println(c);
    }
}
```

上面的例子可以看出结果为5.

### 9.字符串操作符+和+=

该操作符的用途是用来连接不同的字符串.

例如两个字符数即"abc","123",进行字符串连接为"abc"+"123"="abc123"

```java
public class NinePointOne {
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "123";
        System.out.println("s1 + s2:"+(s1+s2));
        // s1 += "1222"   ===>   s1 = s1 + "1223"
        s1 += "1222";
        System.out.println("s1 += :"+s1);
    }
}
```

### 10.类型转化操作符

java允许我们把任何基本数据类型转换成别的基本数据类型,但布尔类型除外,后者不允许进行任何类型的转换处理."类"数据类型不允许进行类型转化.要进行转化要采用特殊的方法,这个在之后介绍.

扩展转化:将容纳更少数据的数据类型转化成能容纳更多数据的数据类型,比如:byte->short->int->long,float->double

```java
public class TenPointOne {
    public static void main(String[] args) {
        int i = 123;
        // 将int转换成long
        long l = (long) i;
    }
}
```

**10.1截尾和舍入**

窄化转化:将能容纳更多信息的数据类型转化成无法容纳那么多信息的类型.

在执行窄化转换时,必须注意结尾和舍入的问题,将float/double->int类型就会出现这个问题.

```java
public class TenPointOne {
    public static void main(String[] args) {
        // 截尾
        double d = 0.123d;
        int num = (int) d;
        System.out.println(num);
    }
}
```

结果为:0,这是因为int类型没有小数,所以会对小数进行截尾操作.

要进行舍入操作要使用java.lang.Math中的round()方法,在[0,0.5)范围舍入0,在[0.5,1]舍入1

```java
public class TenPointOne {
    public static void main(String[] args) {
        // 舍入
        double d1 = 0.49d;
        System.out.println("d1:"+Math.round(d1));
        double d2 = 0.5d;
        System.out.println("d2:"+Math.round(d2));
    }
}
```

结果为:![image-20210509232840354](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210509232840354.png)

## 控制执行流程

### 1.if-else

if(boolean-expresion){

​	statment1;

}else{

​	statment2;

}

当boolean-expresion的值为true时,执行statment1的内容,反之执行statment2的内容.

### 2.迭代

迭代语句分为while,do-while,for

**2.1 for循环**

for(initial ; boolean-expression ; step){

​	statment;

}

```java
public class TwoPointOne {
    public static void main(String[] args) {
        for (int i = 1 ; i <= 5 ; i++){
            System.out.println("第"+i+"次循环");
        }
    }
}
```

结果为:![image-20210510231313003](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210510231313003.png)

**2.2 while与do-while**

do-while的格式:

do 

​	statment;

while(boolean-expression)

while的格式:

while(boolean-expression){

​	statment;

}

do-while与while的区别主要是do-while比while至少会执行一次.

```java
public class TwoPointTwo {
    public static void main(String[] args) {
        int  i  = 1 , j = 1;
        do{
            System.out.println("第"+i+"次执行do-while");
            i++;
        }while (i < 1);

        while (j < 1){
            System.out.println("第"+j+"次执行while");
            j++;
        }
    }
}
```

结果为:![image-20210510232253252](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210510232253252.png)

可见即使波尔表达式的值为false,do-while也会执行一次循环.

### 3.Foreach语法

Java SE5引入了一种新的更简洁的for语法用于数组和容器,即foreach语法

```java
public class ThreePointOne {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5,};
        // for循环
        for (int i = 0; i < array.length; i++){
            System.out.print(array[i]+" ");
        }

        System.out.println();
        System.out.println("============================");
        // foreach
        for (int x : array){
            System.out.print(x+" ");
        }
    }
}
```

结果为:![image-20210511225050346](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210511225050346.png)

### 4.return

return关键字有两个方面的用途:一方面指定一个方法返回什么值,另一个方面它会导致点前的方面退出,并返回那个值.

```java
public class FourPointOne {

    static int test(int i , int j){
        if (i > j){
            return i;
        }else {
            return j;
        }
    }

    public static void main(String[] args) {
        int test = test(1, 2);
        System.out.println(test);
    }
}
```

输出为:2

### 5.break和continue

break用于强制退出循环,不执行循环中的剩余的语句

continue则是停止执行当前的循环,然后退回循环起始处,执行下一次的循环

```java
public class FivePointOne {
    public static void main(String[] args) {
        // break
        int[] array = {1, 2, 3, 4, 5};
        for (int x : array){
            if (x == 2){
                break;
            }
            System.out.print(x+"");
        }
        System.out.println();
        System.out.println("=============");
        // continue
        for (int x : array){
            if (x == 2){
                continue;
            }
            System.out.print(x+"");
        }
    }
}
```

### 6.switch

switch语句的结构:

switch(integral-selector){

​	case integral-value1 : statment1;break;

​	case integral-value2 : statment2;break;

​	default:statment;

}

integral-selector是一个能够产生整数的表达式,switch将这个表达式产生的值与integral-value相比较.若发现相符的,则执行后面的语句,若不相符,则执行default后面的语句.

```java
public class SixPointOne {
    public static void main(String[] args) {
        int index = 0;
        int[] array = {1 , 2, 3, 4, 5};

        for (int i = 0; i < array.length; i++){
            switch (i){
                case 0 :
                    index = i + 1;
                    System.out.println("我是"+array[i]+"在数组中的下标为"+index);
                    break;
                case 1 :
                    index = i + 1;
                    System.out.println("我是"+array[i]+"在数组中的下标为"+index);
                    break;
                case 2 :
                    index = i + 1;
                    System.out.println("我是"+array[i]+"在数组中的下标为"+index);
                    break;
                case 3 :
                    index = i + 1;
                    System.out.println("我是"+array[i]+"在数组中的下标为"+index);
                    break;
                case 4 :
                    index = i + 1;
                    System.out.println("我是"+array[i]+"在数组中的下标为"+index);
                    break;
                default:
                    System.out.println("数据有误");
            }
        }

    }
}
```

## 初始化与清理

### 1.使用构造器进行初始化

在Java中,通过提供构造器,类的设计者可确保每个对象都会得到初始化.创建对象时,如果其类具有构造器,Java就会在用户有能力操作对象之前自动调用相应的构造器,从而确保了初始化的进行.

构造器的如何命名涉及到两个问题.第一,所取的任何名字都可能与类的某个成员名称相冲突;第二,调用构造器是编译器的责任,所以必须让编译器知道应该调用哪个方法.

在Java中,构造器采用与类相同的名称.

不接受任何参数的构造器,叫做**默认构造器**(**无参构造器**).

```java
class One{
    int i;
    int j;

    // 无参构造器
    One(){

    }

    // 有参构造器
    One(int i , int j){
        this.i = i;
        this.j = j;
    }
}
public class OnePointOne {
    public static void main(String[] args) {
        // 通过无参构造器构造对象
        One one1 = new One();
        System.out.println("无参构造器构造对象的存储空间:"+one1);
        // 通过有参构造器构造对象
        One one2 = new One(1, 2);
        System.out.println("对象的属性i的值:"+one2.i);
        System.out.println("对象的属性j的值:"+one2.j);
        System.out.println("有参构造器构造对象的存储空间:"+one2);
    }
}

```

结果是:![image-20210512231142011](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210512231142011.png)

### 2.方法重载

任何的程序设计语言都具备一项重要特性就是对名字的运用.当创建一个对象时,也就给次对象分配到的存储空间取了一个名字.所谓方法则是给某个动作取的名字.通过使用名字,你可以引用所有的对象和方法.

我们知道构造器的名字跟类名是一样的,所有只有一个构造器名,所以当我们想要通过多种的方式创建一个类该怎么办呢?

为了让类的方法同名,就要用到**方法重载**.

```java
class Two{
    int two;
    
    // 重载的构造器
    Two(){
        
    }
    
    Two(int two){
        this.two = two;
    }
    
    // 重载方法
    public void print(int i){
        System.out.println(i);
    }
    
    public void print(String s){
        System.out.println(s);
    }
}
```

**2.1 区分方法重载**

区分方法重载的规则:每各重载方法都必须有一个独一无二的参数类型列表.

```java
class Test{
    
    public void test(int i , int j){
        System.out.println(i+" "+j);
    }
    
    public void test(int i){
        System.out.println(i);
    }
    
    public void test(int i , float f){
        System.out.println(i+" "+f);
    }
}
```

**2.2 涉及基本类型的重载**

基本类型能从一个"较小"的类型自动提升至一个"较大"的类型.

```java
class fun{

    // f的重载
    void f(byte f){
        System.out.println("f(byte)");
    }
    void f(char f){
        System.out.println("f(char)");
    }
    void f(short f){
        System.out.println("f(short)");
    }
    void f(int f){
        System.out.println("f(int)");
    }
    void f(long f){
        System.out.println("f(long)");
    }
    void f(float f){
        System.out.println("f(float)");
    }
    void f(double f){
        System.out.println("f(double)");
    }

    // f1的重载
    void f1(char f){
        System.out.println("f1(char)");
    }
    void f1(short f){
        System.out.println("f1(short)");
    }
    void f1(int f){
        System.out.println("f1(int)");
    }
    void f1(long f){
        System.out.println("f1(long)");
    }
    void f1(float f){
        System.out.println("f1(float)");
    }
    void f1(double f){
        System.out.println("f1(double)");
    }

    // f2的重载
    void f2(int f){
        System.out.println("f2(int)");
    }
    void f2(long f){
        System.out.println("f2(long)");
    }
    void f2(float f){
        System.out.println("f2(float)");
    }
    void f2(double f){
        System.out.println("f2(double)");
    }

    // f3的重载
    void f3(long f){
        System.out.println("f3(long)");
    }
    void f3(float f){
        System.out.println("f3(float)");
    }
    void f3(double f){
        System.out.println("f3(double)");
    }

    // f4的重载
    void f4(float f){
        System.out.println("f4(float)");
    }
    void f4(double f){
        System.out.println("f4(double)");
    }

    //f5的重载
    void f5(double f){
        System.out.println("f5(double)");
    }

    void testF(){
        int i = 10;
        f1(10);
        f2(10);
        f3(10);
        f4(10);
        f5(10);
    }
}

public class TwoPointThree {
    public static void main(String[] args) {
        fun fun = new fun();
        fun.testF();
    }
}
```

结果为:![image-20210513234422745](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210513234422745.png)

从上面的例子可以看出:每个方法都接受的都是一个int型变量,当存在某个重载方法接受int型变量时,它就会被调用,当不存在重载方法不接受int型变量时,如果传入的数据类型小于方法中声明的数据类型,则实际数据类型就会被提升.

char有所不同,当不存在重载方法不接受char型变量时,就会把char提升为int型.

```java
class fun{

    // f的重载
    void f(byte f){
        System.out.println("f(byte)");
    }
    void f(char f){
        System.out.println("f(char)");
    }
    void f(short f){
        System.out.println("f(short)");
    }
    void f(int f){
        System.out.println("f(int)");
    }
    void f(long f){
        System.out.println("f(long)");
    }
    void f(float f){
        System.out.println("f(float)");
    }
    void f(double f){
        System.out.println("f(double)");
    }

    // f1的重载
    void f1(char f){
        System.out.println("f1(char)");
    }
    void f1(short f){
        System.out.println("f1(short)");
    }
    void f1(int f){
        System.out.println("f1(int)");
    }
    void f1(long f){
        System.out.println("f1(long)");
    }
    void f1(float f){
        System.out.println("f1(float)");
    }
    void f1(double f){
        System.out.println("f1(double)");
    }

    // f2的重载
    void f2(int f){
        System.out.println("f2(int)");
    }
    void f2(long f){
        System.out.println("f2(long)");
    }
    void f2(float f){
        System.out.println("f2(float)");
    }
    void f2(double f){
        System.out.println("f2(double)");
    }

    // f3的重载
    void f3(long f){
        System.out.println("f3(long)");
    }
    void f3(float f){
        System.out.println("f3(float)");
    }
    void f3(double f){
        System.out.println("f3(double)");
    }

    // f4的重载
    void f4(float f){
        System.out.println("f4(float)");
    }
    void f4(double f){
        System.out.println("f4(double)");
    }

    //f5的重载
    void f5(double f){
        System.out.println("f5(double)");
    }

    void testChar(){
        char ch = 'x';
        f1(ch);
        f2(ch);
        f3(ch);
        f4(ch);
        f5(ch);
    }
}

public class TwoPointThree {
    public static void main(String[] args) {
        fun fun = new fun();
        fun.testChar();
    }
}
```

结果是:![image-20210513235121783](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210513235121783.png)

### 3.默认构造器

默认构造器又叫作无参构造器,它的作用是创建一个"默认对象".

如果你写的类中没有构造器,则编译器会自动帮你创建一个默认构造器.

如果已经定义了一个构造器(无论是否有参数),编译器就不会帮你自动创建默认构造器.

### 4.this关键字

假设你希望在方法的内部获得当前对象的引用,由于这个引用时编译器传入的,所以没有标识符可以使用.所以有个关键的关键字:this

**this**关键字只能在方法内部使用,表示对"调用方法的那个对象"的引用.

```java
class ThisTest{

    public ThisTest getThisTest(){
        return this;
    }
}
public class FourPointOne {
    public static void main(String[] args) {
        ThisTest thisTest = new ThisTest();
        System.out.println("ThisTest的引用:"+thisTest);
        System.out.println("通过this对ThisTest的引用:"+thisTest.getThisTest());
    }
}
```

结果:![image-20210514231927234](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210514231927234.png)

如果在方法内部调用同一个类的另一个方法,就不必使用this,直接调用即可.因为编译器能自动帮你添加.只有当需要明确指出对当前对象的引用时,才需要使用关键字this.

**4.1 在构造器中调用构造器**

可能一个类写了多个构造器,有时候现在一个构造器中调用另外一个构造器,以避免重复代码.

在构造器中,如果为this添加不同的参数列表,那么就有不同的含义.这将产生对符合此参数列表的某个构造器的明确调用.

```java
class ThisCon{
    int i;
    String s;

    public ThisCon(){
        this(10);  // 调用了有参构造器1
        System.out.println("调用了默认构造器");
    }

    // 有参构造器1
    public ThisCon(int i){
        this(i,"abc");    // 调用了有参构造器2
        System.out.println("调用了有参构造器1");
    }

    // 有参构造器2
    public ThisCon(int i, String s){
        System.out.println("调用了有参构造器2");
    }
}
public class FourPointTwo {
    public static void main(String[] args) {
        ThisCon thisCon = new ThisCon();
    }
}
```

结果为:![image-20210515230342379](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210515230342379.png)

**4.2 static的含义**

static方法就是没有this的方法.在static方法的内部不能调用非静态的方法

### 5.成员初始化

Java尽力保证:所有变量在使用前都能够得到恰当的初始化.

对于类的数据成员(即字段)是基本类型的话都能保证都会有一个初始值.

```java
class MemberInitial{
    byte b;
    char ch;
    boolean bool;
    short sh;
    int i;
    long l;
    float f;
    double d;
    MemberInitial m;

    // 打印初始值
    public void printInitialValue(){
        System.out.println("byte的初始值:"+b);
        System.out.println("char的初始值:"+ch);
        System.out.println("boolean的初始值:"+bool);
        System.out.println("short的初始值:"+sh);
        System.out.println("int的初始值:"+i);
        System.out.println("long的初始值:"+l);
        System.out.println("double的初始值:"+d);
        System.out.println("MemberInitial的初始值:"+m);
    }
}

public class FivePointOne {
    public static void main(String[] args) {
        MemberInitial memberInitial = new MemberInitial();
        memberInitial.printInitialValue();
    }
}
```

结果为:![image-20210516232044054](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210516232044054.png)

从上面可见:char的值是0,所以是空白.在类中定义一个引用变量,如果不进行初始化的话,则这个引用变量就会为null值.

对于方法中的类的数据成员,如果这个数据成员要被使用的话一定要进行赋初值.

**5.1 指定初始化**

如果想为某个变量赋初值的话,有以下三种方法.

方法一:直接在定义类成员变量的地方赋初值

```java
class MemberInitial{
    byte b = 1;
    char ch = 'x';
    boolean bool = true;
    short sh = 1;
    int i = 10;
    long l = 100;
    float f = 0.1f;
    double d = 0.01d;
    MemberInitial m = new MemberInitial();
}
```

方法二:通过调用某个方法进行初始化

```java
class MemberInitial{
    int num;
    
    public int getNum(){
        return 10;
    }
}
```

方法三:这个方法也可以带参数,当这些参数必须是已经初始化了.

```Java 
class MemberInitial{
    char c = getChar('a');
    
    public char getChar(char ch){
        return ch;
    }
}
```

### 6.构造器初始化

可以使用构造器来进行初始化.但要牢记:无法阻止自动初始化的进行,它将在构造器之前发生.

```java
class ConstructorInitial{
    int i;
    ConstructorInitial(){
        System.out.println(i);
        i = 10;
        System.out.println(i);
    }
}
public class SixPointOne {
    public static void main(String[] args) {
        ConstructorInitial constructorInitial = new ConstructorInitial();
    }
}
```

结果为:![image-20210517225740918](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210517225740918.png)

可见在进行构造器初始化之前已经完成了初始化.

**6.1 初始化顺序**

在类的内部,变量定义的顺序决定了初始化的顺序.即使变量定义散布与方法定义之间,它仍然会在任何方法(包括构造器)被调用之前得到初始化.

```java
class ConstructorInitial{
    ConstructorInitial(int initial){
        System.out.println("ConstructorInitial("+initial+")");
    }
}
class InitialTest{
    // 构造器之前的变量
    ConstructorInitial con1 = new ConstructorInitial(1);
    InitialTest(){
        System.out.println("InitialTest");
        // 构造器中的变量
        ConstructorInitial con2 = new ConstructorInitial(2);
    }
    // 构造器后的变量
    ConstructorInitial con3 = new ConstructorInitial(3);
    void initial(){
		System.out.println("initial");
    }
    // 方法后的变量
    ConstructorInitial con4 = new ConstructorInitial(4);
}
public class SixPointOne {
    public static void main(String[] args) {
        InitialTest initialTest = new InitialTest();
        initialTest.initial();
    }
}
```

结果为:![](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210517231106939.png)

可见,无论变量散步在哪里,都会在调用构造器或其他方法之前都到初始化.

**6.2 静态数据的初始化**

无论创建多少个对象,静态资源都只占用一份存储区域.static关键字不能应用于局部变量,因此它只能作用于域.

```java
class StaticInitial{
    StaticInitial(int initial){
        System.out.println("StaticInitial("+initial+")");
    }
    void initial(int initial){
        System.out.println("initial("+initial+")");
    }
}
class StaticInitialOne{
    static StaticInitial staticInitial1 = new StaticInitial(1);
    StaticInitialOne(){
        System.out.println("StaticInitialOne的构造器");
        staticInitial1.initial(1);
    }
    static StaticInitial staticInitial2 = new StaticInitial(2);
}
class StaticInitialTwo{
    StaticInitial staticInitial3 = new StaticInitial(3);
    static StaticInitial staticInitial4 = new StaticInitial(4);
    StaticInitialTwo(){
        System.out.println("StaticInitial的构造器");
        staticInitial4.initial(2);
    }
    static StaticInitial staticInitial5 = new StaticInitial(5);
}

public class SixPointTwo {
    public static void main(String[] args) {
        System.out.println("===================");
        System.out.println("创建StaticInitialOne");
        new StaticInitialOne();
        System.out.println("==================");
        System.out.println("创建StaticInitialTwo");
        new StaticInitialTwo();
    }
    static StaticInitialOne staticInitialOne = new StaticInitialOne();
    static StaticInitialTwo staticInitialTwo = new StaticInitialTwo();
}
```

结果为:![image-20210517233912554](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210517233912554.png)

可见,静态初始化自在必要时刻进行.如果不创建对象,也不引用静态方法,那么静态变量将不会创建.

如果第一个静态变量将被创建之后,它们才会被初始化,此后静态变量不会再次初始化.

初始化的顺序是先静态变量,在是非静态变量.

**6.2 显式的静态初始化**

Java允许多个静态初始化动作组织成一个特殊的"静态子句"(静态代码块)

```java
class StaticCodeBulk{
    static {
        int i = 0;
        int j = 0;
    }
}
```

静态代码块和其他的静态初始化动作一样,这段代码只执行一次:当首次生成这个类的一个对象时,或者首次访问属于那个类的静态数据成员时.

**6.3 非静态实例初始化**

Java也有被称为实例初始化的类似语句,用来初始化每一个对象的非静态变量.

```java
class CodeBulk{
    int i;
    int j;
    {
        i = 1;
        j = 2;
        System.out.println("i:"+i);
        System.out.println("j:"+j);
    }
    CodeBulk(int i, int j){
        this.i = i;
        this.j = j;
        System.out.println("i:"+i);
        System.out.println("j:"+j);
    }
    {
        i = 3;
        j = 4;
        System.out.println("i:"+i);
        System.out.println("j:"+j);
    }
}
public class SixPointFour {
    public static void main(String[] args) {
        CodeBulk codeBulk = new CodeBulk(-1, -2);
    }
}
```

结果为:![image-20210518230210078](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210518230210078.png)

可见,非静态代码块在对象创建之前进行初始化,并且非静态代码块创建一次对象就会初始化一次.

### 7.数组初始化

方式一:特殊初始化,不用new关键字完成,在数组声明的同时完成初始化操作,也被称其为静态初始化.

```java
public class SevenPointOne {
    public static void main(String[] args) {
        // 特殊的初始化
        int[] a1 = {1, 2, 3, 4, 5};
    }
}
```

方式二:先使用new关键字创建数组,然后再分别为数组中的元素赋值,完成初始化操作.

```java
public class SevenPointOne {
    public static void main(String[] args) {
        int[] a2 = new int[5];
        a2[0] = 1;
        a2[1] = 2;
        a2[2] = 3;
        a2[3] = 4;
        a2[4] = 5;
    }
}
```

方式三:使用new关键字创建数组,同时为数组中的元素赋值,完成初始化操作.

```java
public class SevenPointOne {
    public static void main(String[] args) {
        int[] a3 = new int[]{1, 2, 3, 4, 5};
    }
}
```

### 8.可变参数列表

对于应用于参数个数和类型位置的情况下,可以使用可变长参数(如下).

```java
class ArgsTest{

    public void argsTest1(Object... args){
        for (Object obj : args){
            System.out.println(obj);
        }
    }
}
public class EightPointOne {
    public static void main(String[] args) {
        ArgsTest argsTest = new ArgsTest();
        argsTest.argsTest1(new Integer(23),new String("123"),new Float(1.2));
    }
}
```

结果为:![image-20210520230222759](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210520230222759.png)

从上面可以看出可以使用**Object... args**定义一个可变参数列表.由于所有的类都是直接或间接继承了Object类,所以传入参数时可以参数不同的类.传入0个参数也是允许的.

**8.1 除了Object之外的可变参数列表**

```java
class ArgsTest{

    public void argsStringTest(String... args){
        System.out.println("argsStringTest:");
        for (String str : args){
            System.out.println(str);
        }
    }

    public void argsTestInteger(Integer... args){
        System.out.println("argsTestInteger:");
        for (Integer i : args){
            System.out.println(i);
        }
    }

    public void argsTestInt(int... args){
        System.out.println("argsTestInt:");
        for (int i : args){
            System.out.println(i);
        }
    }
}
public class EightPointOne {
    public static void main(String[] args) {
        ArgsTest argsTest = new ArgsTest();
        argsTest.argsStringTest(new String("123"),new String("456"));
        argsTest.argsTestInteger(new Integer(1),new Integer(2));
        argsTest.argsTestInt(new int[]{1,2,3});
    }
}
```

结果为:![image-20210520231146872](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210520231146872.png)

上面的程序已经展示了除Object以外类型的可变参数列表,所以对于**String... args**传入的参数类型必须是String.可见对于包装类型和基本类型也是一样的.

看下面的例子:

```java
class ArgsTest{

    public void argsTestInteger(Integer... args){
        System.out.println("argsTestInteger:");
        for (Integer i : args){
            System.out.println(i);
        }
    }
}
public class EightPointOne {
    public static void main(String[] args) {
      	ArgsTest argsTest = new ArgsTest();
        argsTest.argsTestInteger(4,5,6,7,8);
    }
}
```

结果为:![image-20210520231656524](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210520231656524.png)

从上面可以看出,对于**Integer... args**的可变长形参,可以传入int类型,因为自动编译机制将会将int类型自动装箱到Integer.可见其他的基本类型也是一样的.

## 访问权限控制

### 1.包:库单元

当编写一个Java源代码文件时,此文件通常被称为编译单元,每个编译单元都必须有一个后缀.java,而在编译单元内则可以有一个public类,该类的名称必须与文件的名称相同.

每个编译单元只能有一个public类,否则编译器无法接受.如果在该编译单元之中还有额外的类的话,那么在包之外的世界是无法看见这些类的,因为它们不是public类,而且它们主要是用来为public类提供支持.

**1.1 代码组织**

类库实际上是一组类文件.其中每个文件都有一个public类,以及任意数量的非public类.因此每个文件都有一个构建.如果希望这些构建从属于同一个群组,就可以使用关键字**package**.

任何想要使用该名称的人必须使用前面给出的选择,指定全民或者使用关键字**import**导入相关的包.

### 2.Java访问权限修饰符

public,protected,private这几个是Java访问权限修饰符在使用时,是置于每个每个成员定义之前的(变量,方法,代码块).每个访问权限修饰符仅控制它所修饰的特定定义的访问权.

如果不提供任何权限修饰符,则意味这是"包访问权限".

**2.1 默认访问权限**

默认访问权限没有关键字.

默认访问权限允许将包中所有的类相关联起来,以使他们彼此之间可以相互作用.

**2.2 public权限修饰符**

public用来修饰类中成员变量,成员方法,被public所修饰的成员可以在任何类中都能被访问到.通过操作该类的对象能随意访问public成员.

public在类的继承上的体现,被public所修饰的成员能被所有的子类继承下来.

**2.3 private权限修饰符**

除了包含该成员的类之外,其他任何类都无法访问自各成员.

**2.4 protected权限修饰符**

父类的protected成员是包内可见的,并且对子类可见;

若子类与父类不在同一包中,那么在子类中,子类实例可以访问其从父类继承而来的protected方法，而不能访问父类实例的protected方法.

## 复用类

### 1.组合语法

组合技术:将对象引用置于新类中.

```java
class Combination{
    private int number;
    private double money;
    private String detail;

    Combination(){
        System.out.println("Combination ...");
    }

    @Override
    public String toString() {
        return "Combination{" +
                "number=" + number +
                ", money=" + money +
                ", detail='" + detail + '\'' +
                '}';
    }
}
class CombinationTest{
    Combination combination = new Combination();

    @Override
    public String toString() {
        return "CombinationTest{" +
                "combination=" + combination +
                '}';
    }
}
public class OnePointOne {
    public static void main(String[] args) {
        CombinationTest combinationTest = new CombinationTest();
        System.out.println(combinationTest);
    }
}
```

结果为:![image-20210524231400178](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210524231400178.png)

对象引用会被初始化为null,当你想使用该对象引用调用任何方法时,就会出现空指针异常.

比如:String是引用对象,从上面来看detail为空,当使用detail调用String类中的方法时就会报空指针异常.如下:

```java
class Combination{
    private int number;
    private double money;
    private String detail;

    Combination(){
        System.out.println("Combination ...");
        detail.length();
    }

    @Override
    public String toString() {
        return "Combination{" +
                "number=" + number +
                ", money=" + money +
                ", detail='" + detail + '\'' +
                '}';
    }
}
class CombinationTest{
    Combination combination = new Combination();

    @Override
    public String toString() {
        return "CombinationTest{" +
                "combination=" + combination +
                '}';
    }
}
public class OnePointOne {
    public static void main(String[] args) {
        CombinationTest combinationTest = new CombinationTest();
        System.out.println(combinationTest);
    }
}
```

上面的代码在Combination()构造器中,使用了String类的方法,结果为:

![image-20210524232031502](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210524232031502.png)

为了避免上面的情况,我们可以使用以下的方法进行初始化这些引用:

①在定义对象的地方进行初始化

②在类的构造器中

③就在要使用类对象的前面进行初始化

④使用实例初始化

修改上面的代码验证这四种方法

```java
class Combination{
    private int number;
    private double money;
    private String detail = "abc";  // 在定义对象的地方进行初始化
    private String name;
    private String info;
    private String others;

    Combination(){
        System.out.println("Combination ...");
        System.out.println("detail的长度:"+detail.length());
        this.name = "abc";   // 在类的构造器中
    }

    public void getInfo(){
        // 就在要使用类对象的前面进行初始化
        if (info == null){
            info = "哈哈哈";
        }
        System.out.println("信息简介:"+info);
    }

    {others = "啦啦啦";}  // 使用实例初始化

    @Override
    public String toString() {
        getInfo();
        return "Combination{" +
                "number=" + number +
                ", money=" + money +
                ", detail='" + detail + '\'' +
                ", name='" + name + '\'' +
                ", info='" + info + '\'' +
                ", others='" + others + '\'' +
                '}';
    }
}
class CombinationTest{
    Combination combination = new Combination();


    @Override
    public String toString() {
        return "CombinationTest{" +
                "combination=" + combination +
                '}';
    }
}
public class OnePointOne {
    public static void main(String[] args) {
        CombinationTest combinationTest = new CombinationTest();
        System.out.println(combinationTest);
    }
}
```

结果为:![image-20210524233009691](https://cdn.jsdelivr.net/gh/liyifeizzz/images/img/image-20210524233009691.png)

上面已经使用的四种方法对4个String引用进行初始化.

## 多态

## 接口

## 内部类

## 持有对象

## 通过异常处理错误

## 字符串

## 类型信息

## 泛型

## 数组

## 容器深入研究

## Java I/O系统

## 枚举类型

## 注解

## 并发