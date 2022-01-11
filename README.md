# java12
多态的使用方法、equals和==的不同点
面向对象编程--多态polymorphic
编写一个程序，Master类中有一个feed方法，可以完成主人给动物喂事物的信息

多态基本介绍
方法或对象具有多种形态，是面向对象的第三大特征，多态是建立在封装和继承基础之上的。
多态的具体体现
1.方法的多态
重写和重载就体现多态

多态的具体体现
2.对象的多态（核心）
1.一个对象的编译类型和运行类型可以不一致
2.编译类型在定义对象时，就确定了，不能改变
3.运行类型是可以变化的。
4.编译类型看定义时 = 号的左边，运行类型看 = 号的右边

编译类型                       运行类型
Animal animal = new Dog（);
animal = new Cat()anima的运行类型编程了Cat，编译类型仍然是Animal
public class polyObject {
    public static void main(String[] args) {
        //体验对象多态特点
        //animal 编译类型就是Animal
        Animal01 animal = new Dog();
        animal.cry();//这时即执行该行时，看animal是哪个运行类型（Dog）
       //是Dog所以这个cry是Dog的cry
        //animal 编译类型是Animal，运行类型就是Cat
        animal = new Cat();
        animal.cry();
    }
}


public class Dog extends Animal01 {

    public void cry(){
        System.out.println("Dog cry() 小狗汪汪叫");
    }
}
 class Cat extends Animal01{
    public void cry(){
        System.out.println("Cat cry()小猫喵喵叫");
    }

}

public class Animal01 {

    public void cry(){
        System.out.println("Animal cry()叫");
    }
}
Poly Object

多态的注意事项和细节讨论
多态的前提是：两个对象（类）存在继承关系
多态的向上转型
1.本质：父类的引用指向了子类的对象
2.语法：父类类型 引用名=new 子类类型（）；
3.特点： 编译类型看左边，运行类型看右边。
可以调用父类中的所有成员（需遵循访问权限），
不能调用子类中特有成员；
最终运行效果看子类的具体实现
package com.hspedu.encapsulate.poly_.detail_;

public class polyDetail {
    public static void main(String[] args) {
        //向上转型：父类的引用指向了子类的对象
        //语法：父类类型引用名= new 子类类型
        Animal animal = new Cat();
        Object obj = new Cat();//可以，因为Object也是Cat 的类

        //向上转型调用方法的规则如下
        //可以调用父类中的所有成员（需遵循访问权限）
        //但是不能调用子类的特有的成员
        //因为在编译阶段，能调用哪些成员，是由编译类型来决定的
        animal.sleep();
//        animal.会发现没有Cat的方法，稚嫩调用编译类型里的方法
        //最终的运行效果看子类（运行类型）的具体实现，即调用方法时，按照从子类（运行类型）开始查找
        animal.eat();//猫吃鱼
        animal.run();//跑
        animal.show();//hello,你好
        //编译：javac   运行:java
        //从猫类找eat（）方法，打印出猫里面的eat

    }
}
================
父
package com.hspedu.encapsulate.poly_.detail_;

public class Animal {
    String name;
    int age = 10;
    public void sleep(){
        System.out.println("睡");
    }public void run(){
        System.out.println("跑");
    }public void eat(){
        System.out.println("吃");
    }public void show(){
        System.out.println("hello，你好");
    }
}
================
package com.hspedu.encapsulate.poly_.detail_;

public class Cat extends Animal {
     public void eat(){
         System.out.println("猫吃鱼");
     }public void catchMouse(){
        System.out.println("猫爪老鼠");
    }
  }

面向对象编程- 多态
多态注意事项和细节讨论
多态的向下转型
1语法：子类类型 引用名 = （子类类型）父类引用；
2只能强转父类的引用，不能强转父类的对象
3要求父类的引用必须指向的是当前目标类型的对象
4.可以调用子类类型中所有的成员
package com.hspedu.encapsulate.poly_.detail_;

public class polyDetail {
    public static void main(String[] args) {
        //向上转型：父类的引用指向了子类的对象
        //语法：父类类型引用名= new 子类类型
        Animal animal = new Cat();
        Object obj = new Cat();//可以，因为Object也是Cat 的类

        //向上转型调用方法的规则如下
        //可以调用父类中的所有成员（需遵循访问权限）
        //但是不能调用子类的特有的成员
        //因为在编译阶段，能调用哪些成员，是由编译类型来决定的
        animal.sleep();
//        animal.会发现没有Cat的方法，稚嫩调用编译类型里的方法
        //最终的运行效果看子类（运行类型）的具体实现，即调用方法时，按照从子类（运行类型）开始查找
        animal.eat();//猫吃鱼
        animal.run();//跑
        animal.show();//hello,你好
        //编译：javac   运行:java
        //从猫类找eat（）方法，打印出猫里面的eat
        //老师希望，可以调用cat的catchmouse方法
        //多态的向下转型
        //语法：子类类型 引用名 =（子类类型）父类引用；
        //cat的编译类型 Cat，运行类型是Cat
        Cat cat = (Cat) animal;
        cat.catchMouse();
        //要求父类的引用必须指向的是当前目标类型的对象
        Dog dog = (Dog) animal;//报错Exception in thread "main" java.lang.ClassCastException: com.hspedu.encapsulate.poly_.detail_.Cat cannot be cast to com.hspedu.encapsulate.poly_.detail_.Dog
        //at com.hspedu.encapsulate.poly_.detail_.polyDetail.main(polyDetail.java:29)
    }
//}//结果：睡
//    猫吃鱼
//            跑
//hello，你好
//        猫爪老鼠

package com.hspedu.encapsulate.poly_.detail_;

public class Animal {
    String name;
    int age = 10;
    public void sleep(){
        System.out.println("睡");
    }public void run(){
        System.out.println("跑");
    }public void eat(){
        System.out.println("吃");
    }public void show(){
        System.out.println("hello，你好");
    }
}
public class Cat extends Animal {
     public void eat(){
         System.out.println("猫吃鱼");
     }public void catchMouse(){
        System.out.println("猫爪老鼠");
    }
  }

public class Dog extends Animal {

}
多态注意事项和细节：
属性没有重写之说，属性的值看左边的编译类型（方法看右边的运行类型）

package com.hspedu.encapsulate.poly_.detail_;

public class PolyDetail02 {
    public static void main(String[] args) {
        //属性没有重写之说！属性的值看编译类型
        Base base = new Sub();//向上转型看左边的编译类型
        System.out.println(base.count);//10
        Sub sub = new Sub();
        System.out.println(sub.count);//20


    }
}
class Base{//父类
     int count = 10;


}class Sub extends Base{
    int count = 20;
}

instanceOf比较操作符，用于判断对象的类型是否为XX类型或XX类型的子类型

package com.hspedu.encapsulate.poly_.detail_;

public class PolyDetail03 {
    public static void main(String[] args) {
        BB bb = new BB();
     System.out.println(bb instanceof BB);//true
        System.out.println(bb instanceof AA);//true
        AA aa = new BB();
        System.out.println(aa instanceof AA);//true
        System.out.println(aa instanceof BB);//true 
Object obj = new Object();
        System.out.println(obj instanceof AA);   }
}class AA{}//父类
class BB extends AA{}

java 的动态绑定机制*****
java重要特性：动态绑定机制
1.当调用对象方法的时候，该方法会和该对象的内存地址/云心类型绑定，运行类型里没有找到方法的话用父类的方法，
2.当调用对象属性时，没有动态绑定机制，哪里声明，哪里使用 int i =5；


class A{
 int i = 5
public  int sum(){
get()}
class B(){
int j = 6 
public int get(){
     return  j+  5}    
   
}
}
多态的应用
1.多态数组
数组的定义类型为父类类型，里面保存的实际元素类型为子类类型
应用实例：现有一个继承结构如下：要求创建一个Person对象，2个strudent 对象和2个Teacher对象，统一放在数组中，并调用每个对象
say方法
public class PolyArray {
    public static void main(String[] args) {


    //要求创建一个Person对象，2个strudent 对象和
    // 2个Teacher对象，统一放在数组中，并调用每个对象
    Person[]persons = new Person[5];
    persons[0]= new Person("jack",20);
    persons[1]= new Student("jack",18,100);
    persons[2]= new Student("smith",19,30.1);
    persons[3]= new Teacher("scott",30,20000);
    persons[4]= new Teacher("king",50,25000);
        for (int i = 0; i < persons.length; i++) {
            //老是提示：person[i] 编译类型是Person，运行类型是根据实际情况JVM来判断
              //动态绑定机制
            System.out.println(persons[i].say());
        }
    }
}
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }public String say(){
        return name + "\t";
    }

public class Student extends Person{
    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }//重写父类say方法

    @Override
    public String say() {
        return super.say() + "score=" + score;
    }
}

public class Teacher extends Person{
    private double salary;

    public Teacher(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;

    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String say() {
        return super.say() + salary;
    }
}


应用实例升级：如何调用子类特有的方法，比如Teacher 有一个teach， Student 有一个study怎么调用

package com.hspedu.encapsulate.poly_.polyarr_;

public class PolyArray {
    public static void main(String[] args) {


    //要求创建一个Person对象，2个strudent 对象和
    // 2个Teacher对象，统一放在数组中，并调用每个对象
    Person[]persons = new Person[5];
    persons[0]= new Person("jack",20);
    persons[1]= new Student("jack",18,100);
    persons[2]= new Student("smith",19,30.1);
    persons[3]= new Teacher("scott",30,20000);
    persons[4]= new Teacher("king",50,25000);
        for (int i = 0; i < persons.length; i++) {
            //老是提示：person[i] 编译类型是Person，运行类型是根据实际情况JVM来判断
              //动态绑定机制
            System.out.println(persons[i].say());
            //不能调用study和teach
            //这里大家聪明想一想
            if (persons[i] instanceof Student) {
                Student student = (Student)persons[i];
                student.study();
//            也可以写成和成一步 （(Student)persons[i]）.study();
            }else if(persons[i] instanceof  Teacher ){
                Teacher teacher = (Teacher)persons[i];
                teacher.teach();

            }else if(persons[i] instanceof Person){

            } else{
                System.out.println("你的类型有误，请自己检查");
            }

        }
    }
}


public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }public String say(){
        return name + "\t";
    }

}



public class Student extends Person{
    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }//重写父类say方法

    @Override
    public String say() {
        return super.say() + "score=" + score;
    }public void study(){
        System.out.println("学生"+ getName()+"学习");
    }
}



public class Teacher extends Person{
    private double salary;

    public Teacher(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;

    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String say() {
        return super.say() + salary;
    }public void teach(){
        System.out.println("老师"+getName()+"正在讲课");
    }
}

2.多态参数
方法定义的形参类型为父类类型，实参类型允许为子类类型
应用实例1，前面的主人喂动物
应用实例2，定义员工类Emoloyee，包含姓名和月工资【private】，以及计算年工资getAnnual的方法。普通员工和经理继承了员工，经理类多了资金bonus属性和管理manage方法，普通员工类多了work方法，普通员工和经理类要求分别重写getAnnual方法
测试类中添加一个方法showEmpAnnal（Employee e），实现获取任何员工对象的年工资，并在main方法中调用该方法

测试类中添加一个方法，testWork，如果是普通员工，则调用work方法，如果是经理，则调用manage方法 



package com.hspedu.encapsulate.polyparameter_;

public class PolyParameter {
    public static void main(String[] args) {
        NormalEmployee zhengdaoxuan = new NormalEmployee("zhengdaoxuan", 500000);
        manage milan = new manage("milan", 2000, 3000);

        PolyParameter polyParameter = new PolyParameter();
        polyParameter.showEmpAnnual(zhengdaoxuan);
        polyParameter.showEmpAnnual(milan);
        polyParameter.testWork(zhengdaoxuan);
        polyParameter.testWork(milan);
    }public void showEmpAnnual(Employee e){
        System.out.println(e.getAnnual());//动态绑定机制
    }//添加一个方法，testWork，如果是普通员工，则调用work方法，如果是经理，则调用manage方法
    public void testWork(Employee e){
        if (e instanceof NormalEmployee) {
           ((NormalEmployee) e).work();//有向下转型操作强转


        }else if(e instanceof manage){
            ((manage)e).manage();//有向下转型操作强转
        }else{
            System.out.println("不做处理");
        }
    }
}

package com.hspedu.encapsulate.polyparameter_;

public class Employee {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public double getAnnual() {
        return 12 * salary;
    }


    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
}


package com.hspedu.encapsulate.polyparameter_;

public class manage extends Employee{
   private double bonus;


    public manage(String name, double salary, double bonus) {
        super(name, salary);
        this.bonus = bonus;
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }
    public void manage(){
        System.out.println("经理" + getName() + "is manageing");
    }

    @Override
    public double getAnnual() {
        return super.getAnnual() + bonus;
    }
}

package com.hspedu.encapsulate.polyparameter_;

public class NormalEmployee extends Employee{

    public void work(){

    }

    public NormalEmployee(String name, double salary) {
        super(name, salary);

    }

    @Override
    public double getAnnual() {//因为普通员工没有其他收入，则直接调用父类方法
        return super.getAnnual();
    }


}

Object
equals方法
==和equals的对比
1.==：既可以判断基本类型，又可以判断引用类型，
2.==：如果判断基本类型，判断的是值是否相等。实例：int i = 10； double d = 10.0；
3.==：如果判断引用类型，判断的是地址是否相等，即判定是不是同一个对象


public class Equals01 {
    public static void main(String[] args) {
        AC a = new AC();
        AC b = a;
        AC c = b;
        System.out.println(a == c);//true
        B cd = a;
        System.out.println(cd == c);//true

    }
}
class B{}
class AC extends B{ }


equals方法
4.equals：是Object类中的方法，只能判断引用类型，如何看JDK原码  比如Integer，String
查看equals原码输入ctrl + b


5.默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等。
package com.hspedu.encapsulate.Equals01;

import com.hspedu.encapsulate.super_.A;

public class Equals01 {
    public static void main(String[] args) {
        AC a = new AC();
        AC b = a;
        AC c = b;
        System.out.println(a == c);//true因为new 一个AC地址指向的地址是相同的
        B cd = a;
        System.out.println(cd == c);//true
        int num1 = 10;
        double num2 = 10.0;
        System.out.println(num1 == num2);
        "hello".equals("abc");
            Integer integer = A

//           equals 原码           对象
//        public boolean equals(Object anObject) {
//            if (this == anObject) { 如果是同一个对象地址，两个引用类型看的是地址是否相等
//                return true;
//            }
//            if (anObject instanceof String) {是否是String类型的子类
//                String anotherString = (String)anObject;向下转型
//                int n = value.length;
//                if (n == anotherString.value.length) {如果字符串长度相同
//                    char v1[] = value;
//                    char v2[] = anotherString.value;
//                    int i = 0;
//                    while (n-- != 0) {//然后一个一个的比较字符
//                        if (v1[i] != v2[i])
//                            return false;
//                        i++;
//                    }
//                    return true;如果两个字符串的所有字符都相等，则返回true
//                }
//            }
//            return false;//如果比较的不是字符串，则直接返回false
        //看看Object 的类的equals是
        //即Object 的equals 方法默认就是比较对象地址是否相同
        //equals把Object 的equals方法重写了，编程了比较两个字符串
//        public boolean eauqls (Object obj){
//            return (this == obj);






//从原吗可以看到 Integer 也重写Object的equals方法
        //变成了判断两个值是否相同


//        public boolean equals(Object obj) {
//            if (obj instanceof Integer) {
//                return value == ((Integer)obj).intValue();
//            }
//            return false;
        Integer integer1 = new Integer(10000);
        Integer integer2 = new Integer(10000);
        System.out.println(integer1 == integer2);//false 因为new 开辟的空间内存不是一个地方
        System.out.println(integer1.equals(integer2));//true 因为判断的是值
        String str1 = new String("hspedu");
        String str2 = new String("hspedu");
        System.out.println(str1 == str2);//false
        System.out.println(str1.equals(str2));//true


        }
//        }

//        }


    }
}
class B{}
class AC extends B{ }

如何重写equals方法
应用实例：判断两个Person对象的内容是否相等，如果两个Person对象的各个属性值都一样，则返回true，反之false

package com.hspedu.encapsulate.Equals01;

public class EqualsExercise01 {
    public static void main(String[] args) {
        Person p1 = new Person("jack",18,'1');
        Person p2 = new Person("jack",18,'1');
        System.out.println(p1.equals(p2));

    }
}class Person{
    private String name;
    private int age;
    private char gender;

    public Person(String name, int age, char gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public char getGender() {
        return gender;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }




    public boolean equals(Object obj){
        if (this == obj) {
            //判断如果比较的两个对象时同一个对象，则直接返回true
    return  true;
 }
        if (obj instanceof Person) {//类型是Person才比较
       //进行向下转型
            Person p = (Person)obj;//向下转型
            return this.name.equals(p.name)&&this.age == p.age && this.gender == p.gender;

        }
        //如果不是Person，则直接返回false
        return false;


    }
}

Person p1 = new Person()
Person p2 = new Person()
p1.name = "a"
p2.name = "a"
p1==p2 false  指向 地址
p1.name equals(p2.name)true 内容变字符

String s1 = new String ("asdf")
String s2 = new String(“asdf“)
s1.equals(s2)
equals 被重写了被String重写了本来是Object    String里的子类有equals














