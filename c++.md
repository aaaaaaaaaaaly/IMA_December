# c++

## const

**常量指针  const int*p=&a**

常量指针只是不能通过指针修改变量值，可以直接将变量赋值来达到修改的目的（即不能通过*p解引用来修改值），指针指向的地址可以直接改。



**指针常量 int* const p=&a**

指向的地址不能改，但是可以更改值



**加深理解**

const修饰的东西不能改。

const int* p ，const修饰的是p指向的值；

int* const p const修饰 的是地址。



## 指针和数组

### 利用指针访问数组中的元素

“*****”的运算优先级高于“+”

```c++
int arr[10]={1,2,3,4,5,6,7,8,9,10}
for i=0;
int* p=arr;
for(;i<10;i++)
{
    printf("%d",*p);
    p++;//指针加加，是用步数*数据类型，让地址向后移动
    //如果要所指向的值加加，应该表示为 *p++
    //须知：*num+1 ！= *（num+1），前者默认*数据类型
}
```

### 结构体创建和使用

```c++
# include <iostream>
# include<string>//c++要用到字符串，需要包含头文件 string
using namespace std;
//创建数据类型
	//实现各种数据类型的集合
struct student
{
	string name;
	int age;
	int score;
}s3;
//在结构体定义的时候顺便定义变量
int main()
{
	//创建具体学生
	//创建具体学生的时候，struct关键字可以省略，比如student s1；
	struct student s1;
	s1.name = "ashely";
	s1.age = 18;
	s1.score = 100;
	cout << "name: " << s1.name << "  age:" << s1.age << "   score:" << s1.score<<endl;
	//  2.2  struct student s2 ={};
      struct student s2 ={"li",20,100};
	  cout << "name: " << s2.name << "  age:" << s2.age << "   score:" << s2.score<<endl;

	system("pause");
	return 0;
}
```

### 结构体数组以及结构体指针

```c++
# include<iostream>
# include<string>
using namespace std;
//define 
struct student
{
	string name;
	int age;
	int score;
};
int main()
{
	//bulid 结构体数组
	struct student stuarry[3] =
	{
		{"a",18,98},
		{"b",19,99},
		{"c",10,100}
	};
	int i = 0;
	//for (; i < 3; i++)
	//{
		//cout << "name:" << stuarry[i].name << " age:" << stuarry[i].age << " score:" << stuarry[i].score << endl;
	//}
	//rebuild
	//stuarry[0].name = "ashely";
	//stuarry[1].score = 100;
	//cout << endl;
	//i = 0;
	//for (; i < 3; i++)
	//{
		//cout << "name:" << stuarry[i].name << " age:" << stuarry[i].age << " score:" << stuarry[i].score << endl;
	//}

	//结构体指针
	//通过结构体指针访问，需要使用箭头来访问属性，且注意数据类型的要求 应该是自定义的结构
	student s2 = { "MING",18,100 };
	student* p = &s2;
	cout << "name:" << p->name << "  age:" << p->age << "  score:" << p->score << endl;
	system("pause");
	return 0;
}
```

### 结构体镶嵌使用

```c++
# include <iostream>
# include<string>
using namespace std;
struct student
{
	string name;
	int age;
	int score;
};
struct teacher
{
	int id;
	string name;
	int age;
	struct student s1;//表示创建一个老师对应的学生
};
//创建一个打印学生信息的函数
void prinstudent1(struct student s)//值传递
{
	cout << "name:" << s.name << " age:" << s.age << " score:" << s.score << endl;
}
void prinstudent2(struct student* s)//地址传递
{
	s->name = "ashely";  //通过指针改变
	cout << "name:" << s->name << " age:" << s->age << " score:" << s->score << endl;
}
int main()
{
	teacher t1;
	t1.id = 10010;
	t1.name = "white";
	t1.age = 32;
	t1.s1.name = "ming";
	t1.s1.age = 11;
	t1.s1.score = 99;
	cout << "老师的姓名:" << t1.name << "  老师辅导的学生姓名：" << t1.s1.name << "  学生分数：" << t1.s1.score << endl;

	//结构体做函数参数
	//将学生传到一个参数中，打印学生身上的所有信息，利用前面已经创建的结构体
	student s2{ "li",20,100 };
	student* p2 = &s2;
	prinstudent1(s2);
	prinstudent2(p2);
	cout << "name:" << s2.name << " age:" << s2.age << " score:" <<s2.score << endl;
	system("pause");
	return 0;
}
```

### 结构体中const的使用场景

```c++
# include<iostream>
# include<string>
using namespace std;
struct student
{
	string name;
	int age;
	int score;
};
//地址传递有隐患，如果在函数里面误操作，值就直接全部改变
//把 student*s 改为 const student*s
//改成指针能节省空间，如果只是单纯传值copy全部，内存浪费
void prin(const student* s)
{
	cout << s->name << "  " << s->age << "  " << s->score << endl;
}
int main()
{
	student s1{ "i",19,100 };
	student* p = &s1;
	prin(p);
	system("pause");
	return 0;
}
```

## 通讯录管理系统

#### 菜单功能

#### 退出功能

#### 添加联系人

```c++
system("pause")
system("cls")//清屏操作
```

功能描述：有人数上限，联系人信息包括姓名，性别，年龄，联系电话，家庭住址



实现步骤：

- 设计联系人结构体
- 设计通讯录结构体
- main（）函数中创建通讯录
- 封装添加联系人函数
- 测试添加联系人功能

1. 设计联系人结构体：

```c++
# define Max 1000
struct ADD
{
    struct person [Max];//通讯录中保存联系人数组
    int p_size;//通讯录中的人员个数
}
```



#### 删除联系人

#### 查找联系人

#### 修改联系人

#### 清空联系人

## 进阶基础

#### 内存4个区域

- 代码区：存放函数体的二进制代码，由操作系统管理
- 全局区：存放全局变量，静态变量，常量
- 栈区：编译器自动分配释放，存放函数的参数值，局部变量等
- 堆区：由程序员分配和释放，若程序员不释放，程序结束时由操作系统回收

#### 程序运行前

程序编译后，生成exe可执行程序，未执行该程序前分为2个区域

**代码区：**

​           存放cpu执行的机器命令

​           共享，对于被频繁执行的程序，只需要在内存中放一份即可

​           只读，防止程序意外修改指令

**全局区**：

1. ​            全局变量和静态变量

2. ​            全局区还包括常量区，字符串常量和其他常量：          

3. ```
   静态变量：
   int main()
   {
   局部变量:int a=0;
   
   静态变量:static int b=0;
   
   常量:
   
   字符串常量，即“ ”引起来的变量
   string a="hello world"
   
   const修饰的变量
   const修饰的变量： 即在main外部设置： const int a=0;
   const修饰的全局变量：即在main外部设置： const int b=0;
   const修饰的局部变量：即在main内部设置： const int c=0;
   }
   查看各自的地址比较远近，可以大体感受是否在全局区
   
   总结：全局变量，静态变量（static），
        字符串常量，const修饰的全局变量，以上在全局区
   ```

4. ​           **该区域的数据在程序结束后释放**

#### 程序运行后

**栈区**：

​            由编译器自动分配释放

​            注意：**不要返回局部变量的地址**

```
int* func()
{
int a=0;  //局部变量，存放在栈区，栈区的数据在函数执行完后自动释放
return &a;  //返回局部变量的地址
}
int mian()
{
int* p=func();
cout<<*p<<endl;//第一次能够正常表示，这是因为系统会临时存放
cout<<*p<<endl;//第二次就不能正常表示，因为前面已经表示了那个临时存放的值
}
```

​           

**堆区：**

程序员分配释放，如果程序员不释放，程序结束的时候有操作系统回收

c++主要利用 new 在堆区中开辟数据：

```
int* func()
{
//利用new关键字，可以将数据开辟到堆区
//这里的p还是局部变量，存放在栈区，而指向的是堆区的数据
//而堆区是由程序员管理的
int* p=new int(10);
return p;
}
int main()
{
int*p=func();
cout<<*p<<endl;
return 0;
}
```

**new操作符**

利用 **new 操作符**在堆区中开辟数据

释放利用操作符 **delete**

```
基本语法：
int* func()
{
在堆区创建整数数据

new返回的是该类型的指针
int* p=new int (10);

return p;
}


void func2()
{
int* p=func();
cout<<*p<<endl;
delete p;       //释放
}
```

```
在堆区利用 new 开辟数组：  (因为new返回的是指针，数组本质就是指针)
void func3()
{
//创建堆区数组
int* arr=new int [10];

for(int i=0;i<10;i++)
{
   cout<<arr[i]<<endl;
}
//释放数组，得在delete后加一个[]，告诉系统这是一串数
delete[] arr;
}
```

## 引用

给变量期别名

语法： 数据类型 &别名 = 原名

```
int a=0；
int &b =a；//给a一个别名
b=20;
cout<<a<<endl;

a==20;
```

#### 注意事项：

- 引用必须初始化
- 引用在初始化后，不可以改变

```
int a=10;
int &b=a;
//必须在 &b 初始化的时候，表明是哪一个变量的别名

//初始化后，b不能是别人的别名

int a=0;
int &b =a;
int c=10;
b=c;

!注意，这里的 b=c 是赋值操作，所以是没问题的
```

#### 引用做函数参数

作用：函数传参，利用引用可以让**形参修饰实参**

优点：可以简化**指针修改实参**

```
//交换函数

//1,值传递
void swap1(int a,int b)
{
int temp;
int temp=a;
int a=b;
int b=temp;
}
//2,地址传递
void swap2(int* a,int* b)//地址传递，形参会修饰实参
{
int temp;
temp=*a;
*a=*b;
*b=temp;
}
//3,引用传递
void swap3(int &a,int&b)  //这里的a,b就是主函数里面a，b的别名
{
int temp;//别名进行赋值
temp=a;
a=b;
b=temp;
}
//主函数
int main()
{
int a=10;
int b=9;
swap1(a,b);
swap2(&a,&b);
swap3(a,b);
return 0；
}
```

#### 引用做函数的返回值

**注意事项：**

- 不要返回局部变量的引用
- 函数的调用可以作为左值

```
error 的操作：
//自定义函数
int& test1()
{
int a=20; //局部变量存放在栈区
return a;
}
//主函数
it mian()
{
int &ref =test1(); //引用语法 int &b =a；
return 0；
}
```

```
正确：
//自定义函数
int& test2()
{
static int a=20; //静态变量存放在全局区，程序结束运行才被释放
return a;
}
//主函数
it mian()
{
int &ref =test1(); //引用语法 int &b =a；
return 0；
}
```

```
可以作为左值，以上面正确的程序为例
//自定义函数
int& test2()
{
static int a=20; //静态变量存放在全局区，程序结束运行才被释放
return a;
}
//主函数
int main()
{
int &ref2=test2()
cout<<ref2<<endl;     //--->  20

test2=1000;//相当于把a赋值为 1000
cout<<ref2<<endl;       //---> 1000
cout<<ref2<<endl;       //---> 1000
}

//所以，如果函数的返回是引用，这个函数的调用可以作为左值被赋值，影响到同时是别名和那个被引用的变量
```

#### 引用的本质

本质：引用的本质是一个**指针常量**（int* const p）

```c++
int mian()
{
int a=10;
//自动转化 int* const ref =&a; 指针常量是指指针的指向不可改
int &ref =a;
ref=10;//内部发现ref是引用，自动帮我们转化为： *ref=20
return 0;
}
```

#### 常量引用

作用：常量引用主要用来修饰形参，防止误操作

在函数形参列表中，可以加const修饰形参，繁殖形参改变实参

```
error：
int main()
{
int a=10;
int &ref =10;//10是自变量，不能直接给ref，必须引用一块合法的空间
}
```

```
正确：
int main()
{
 int a=10;
 const int &ref =10;
}

//加const之后，编译器将代码修改为：
int temp=10；
const int &ref =temp;
//加入const之后变成常量指针，不能重新赋值
```

```
打印函数
void show(int &val)
{
cout<<val<<endl;     ->100
}
int mian()
{
int a=100;
show(a);
return 0;
}
```

```
打印函数2
void show(const int &val)
{
val=1000; //error报错     //如果在函数里面修改了引用，
cout<<val<<endl;     ->1000
}
int mian()
{
int a=100;
show(a);
cout<<a<<endl;       ->1000
return 0;
}
```

## 函数提高

#### 函数默认参数

函数形参列表中的形参可以有默认值

语法：返回值类型 函数名 (参数+默认值) {}

```
int func (int a, int b=20, int c=30)
{
return a+b+c;
}
int main()
{
cout<<func(10)<<endl;  ->30
cout<<func(10,30)<<endl;  ->70
return 0;
}
```

**注意事项：**

1. 如果某个位置已经有了默认值，那么从这个位置往后，从左到右必须有默认值
2. 如果函数声明有默认值，函数实现的时候就不能有默认参数

```
int func2(int a=10,int b=10);//声明
int func2(int a ,int b)//函数实现
{
return a+b;
}
```

#### 函数占位参数

语法： 返回值类型 函数名 （数据类型）{}

占位参数也可以有默认参数

```
yoid func(int ,int)
{
cout <<"hello,world"<<endl;
}
int main()
{
funv(10,10);
return 0;
}
```

#### 函数重载

作用：函数名可以相同，提高复用性

**函数重载满足条件：**

- 同一个作用域下面
- 函数名称相同
- 函数参数**类型不同** 或者 **个数不同** 或者 **顺序不同*

**注意事项：**

- 引用作为函数重载的条件
- 函数重载碰到函数默认参数

## 类

**封装，继承，多态**

#### 封装

类和结构体类似，主要区别在于，**成员属性的权限设置**，成员包括数据成员，成员函数，构造函数（可以重载）

##### 将成员属性设置为私有

```c++
class person
{
    public:
    void setname(string name)
    {
        Name=name;
    }
    string getname
    {
        return Name;
    }
    private:
    string Name;
    int age;
    string lover;
};
int main()
{
    person p1;
    p1.setname("ashelly");
    cout<<"name: "<<p1.Name<<endl;
    return 0;
}
```

权限的 设置可以来控制 **读，写**的设置

创建立方体类的流程：

- 创建
- 设计属性
- 设计行为 （函数获取立方体的面积和体积）

- **分别**利用**全局函数**和**成员函数** 判断两个立方体是否相等

头文件声明

源文件实现:heart:

A:: B表示B是A作用域下的函数

```c++

//比如设置一个 立方体类
class cube
{
    public://公共
    //行为
    //设置长宽高
    //获取立方体的面积
    //获取立方体的体积
    private://私有
    //属性
    //L=
    //W=
    //H=
}
```

##### 案例：立方体类

```c++
# include<iostream>
using namespace std;
//立方体的设计
//创建类
//设计属性
//设计行为获取立方体的面积和体积‘分别利用全局函数和成员函数判断两个立方体是否相等
class cube
{
public:
	//设置长
	void setl(int L)
	{
		 l = L;
	}//把传入的长度赋值给类内代表相应属性的成员
	//获取长
	int getl()
	{
		return l;//返回这个成员属性，让外部获取
	}
	//类似的，设置宽和高
	void setw(int W)
	{
		 w = W;
	}
	int getw()
	{
		return w;
	}
	void seth(int H)
	{
		 h = H;
	}
	int geth()
	{
		return h;
	}
	int  calculates()
	{
		return (l * h + l * w + h * w) * 2;
	}
	int calculatev()
	{
		return h * l * w;
	}
private:
	int l;
	int w;
	int h;
};
int main()
{
	cube c1;//创建
	c1.setl(10);
	c1.setw(10);
	c1.seth(10);
	cout << c1.calculates() << endl;
	cout << c1.calculatev() << endl;
	system("pause");
	return 0;
}
```

- :hear_no_evil:遇到一个问题，public里面获取外部传入的长度时，如果写成`int l=L`,最后的结果溢出，如果直接`l=L`结果正确。private里面已近定义了`int l;int w;int h;`
- 内部的函数等可以访问所有成员，`private` 禁止外部访问



#### 对象的初始化和清理

##### 构造函数和析构函数

初始化和清理是两个很重要的安全问题，使用一个对象和变量，没有及时清理，也会造成安全问题

如果我们不自己提供这两个函数，编译器提供这两个函数的空实现



> 构造函数：作用于创建对象时为对象的成员属性赋值，构造函由编译器调用

> 析构函数：作用于对象销毁前的系统自动调用，执行一些清理工作



构造函数语法` 类名( ) { }`

1. 没有返回值也不写void
2. 函数名称与类名相同
3. 可以有参数，因此可以发生重载
4. 程序在调用对象的时候自动调用构造函数，无需手动，而且只会调用一次

构析函数语法 ``类名 ( ) { }`

1. 没有返回值也不写void

2. 函数名称与类名相同,**在名称前面加上符号`**

3. **不**可以有参数，因此**不**可以发生重载

4. 程序在调用对象的时候自动调用构造函数，无需手动，而且只会调用一次

   ```c++
   # include<iostream>
   using namespace std;
   class person
   {
   public:
   	//构造函数
   	//没有返回值，
   	//有参数，函数名和类的名称相同
   	person()
   	{
   		cout << "person" << endl;
   	}
   	//没有返回值没有参数，前面加波浪，对象在销毁前调用，且调用一次
   	~person()
   	{
   		cout << "pperson" << endl;
   	}
   };
   void test01()//局部变量 在栈区 test01在执行完毕后，释放这个对象
   {
   	person p;
   }
   int main()
   {
   	test01();//创建对象会被自动调用(即使没有输出命令)，且只调用一次
   	system("pause");
   	return 0;
   ```

   

##### 构造函数的分类和调用

**两种**分类方式：

- 按参数分类：有无参数
- 按类型分类：普通构造和拷贝构造

**三种**调用方式：

- 括号法
- 显示法
- 隐式转换法

**拷贝构造函数语法：**

` 类名(const 类名 &对象名) `

按照**引用**的方式传入



##### 构造函数调用规则

###### 基础：

默认情况下，c++编译器至少给一个类添加3个函数

- 默认构造函数（无参），函数体为空
- 默认构析函数（无参），函数体为空
- 默认拷贝构造函数，对属性进行**值**拷贝



###### 构造函数调用规则：

- 如果用户定义有参构造函数，c++不在提供无参构造，但是会提供**默认拷贝函数**
- 如果用户定义拷贝构造函数，c++不会再提供其他构造函数
- 如果我们设置了拷贝构造函数，编译器就不再提供其他默认函数，所以其他的也要自己设置



```c
//构造函数 (空)
//构析函数(空)
//拷贝构造函数(值拷贝)
class person//类
{
    public:
    person()
    {
        cout<<"无参构造"<<endl;
    }
     person(int  age)
    {
        cout<<"有参构造"<<endl;
    }
     person(const person &p)//拷贝构造函数
    {
          cout<<"拷贝构造"<<endl;
       age=p.age;
    }
};
void test01 ()
{
    person p;
    p.age=18；
     
    person p2(p);
    cout<<"p2年龄： "<<p2.age<<endl;
}

//- 如果用户定义有参构造函数，c++不在提供无参构造，但是会提供默认拷贝函数
    
void test02()
{
    person p;//调用无参构造，因为当自己定义使用了有参构造函数（此时编译器不再提供默认构造函数），且自己不再定义无参构造，报错
    person (18);
    person p2(p);
}
int main()
{
    test01 ();
    test02 ();
    return 0;
}
```



###### 总结：

定义了有参构造，编译器不再提供无参构造，要自己定义

定义了拷贝构造，编译器不再提供其他构造函数，要自己定义



##### 深拷贝和浅拷贝

###### 基础：

浅拷贝：简单的赋值拷贝操作

深拷贝：早堆区重新申请空间，进行拷贝操作



###### 示例：

**浅拷贝**，直接赋值拷贝操作

```c
# include<iostream>
# include<string>
using namespace std;
class person
{
public:
	person()
	{
		cout << "默认构造函数调用" << endl;
	}
	person(int age)
	{
		Age = age;
		cout << "有参构造函数调用" << endl;
	}
	~person()
	{
		cout << "析构函数调用" << endl;
	}
	int Age;
};
void test01()
{
	person p1(18);
	cout << "p1 age :" << p1.Age << endl;
    person p1(p2)
}
int main()
{
	test01();
	system("pause");
	return 0;
}


//则在 test 内使用 person p1(p2)可以实现
//因为系统会默认 浅拷贝的实现，（虽然我没提过拷贝构造函数

```

**深拷贝**：堆区开辟，开辟用**new(  )**  需要自己 (在构析函数中）释放free( )，**delete（ ）**

```c
# include<iostream>
# include<string>
using namespace std;
class person
{
public:
	person()
	{
		cout << "默认构造函数调用" << endl;
	}
    
    //有参构造函数
	person(int age,int height)
	{
        Height=new int (height);//new()返回值为指针
		Age = age;
		cout << "有参构造函数调用" << endl;
	}
    
    
    //释放空间
   //析构函数
	~person()//程序结束前的最后一步
	{
        if(Height_!=NULL)//指针不是野指针
        {
            delete Height;
            Height=NuLL:
         }
		cout << "析构函数调用" << endl;
	}
    
    
    //拷贝函数，深拷贝
    person(const person &p)//引用
    {
        Height=new int (*p.Height);//重新在堆区创造一块空间,然后把传入的p的Height的值赋给这块新的空间，原本自己的指针指向这块空间
    }
	int Age;
    int* Height;
};
void test01()
{
	person p1(18,160);
	cout << "p1 age :" << p1.Age << endl;
    cout << "身高"  <<*p1.Height << endl;//height是指针，所以要打印值需要解引用
    person p1(p2);
    cout << "身高"  <<*p2.Height << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

- 堆区的内层重复是否则会报错，都使用了释放，利用判断（if Height  ！=NULL）

:hand:height是指针，所以要打印值需要解引用，和简单拷贝的区别在于，深拷贝在堆区开辟一块空间给Height

:high_brightness:new( )返回值是指针



##### 初始化列表

###### 作用：

c++提供了初始化列表的语法，用来初始化属性

###### 语法

`构造函数( ): 属性1（值1），属性2（值2）......{ }`

###### 示例：

```c
# include<iostream>
# include<string>
using namespace std;
class person
{
public:
	//初始化操作
	//person(int a, int b, int c)
	//{
	//	 A = a;
	//	 B = b;
	//	 C = c;
	//}

	//初始化列表初始化属性
	//person() :A(10), B(20), C(30)
	//{

	//}
    //初始化列表初始化属性的灵活运用，让赋值更灵活
	person(int a,int b,int c) :A(a), B(b), C(c)//更灵活，可以在主函数的调用中有用户定义
	{

	}
	int A, B, C;
};
void test01()
{
	//person p(10,20,30);
	//person p;
	person p(10, 30, 20);
	cout << p.A << " " << p.B << " " << p.C << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```



##### 类对象作为类成员

c++类中的成员可以是另一个类的对象，我们称该成员为 **对象成员**



例如

**类似结构体里面的结构体**

```c
class A{}
class B//类似结构体里面的结构体
{
    A a;
}
```

B类中有对象A作为成员，A为对象成员



```c
# include<iostream>
# include<string>
using namespace std;
class phone
{
	string name;
	int year;

	//行为
	void Phone(string pname)
	{
		name = pname;
	}
};
class person
{
public:
	person(string name, string phone) :name(name), phone.name(phone)
	{

	}
	string name;
	phone phone;
};
void test01()
{

}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

构造函数的顺序：当其他类对象作为本类成员，构造时候先构造类对象，再构造自身

析构函数的顺序：和构造函数的顺序相反。先构造自身，再构造其他对象



##### 静态成员

###### 基础

静态成员就是在成员变量和成员函数前加上关键词 **static**，称为静态成员

静态成员分为：

- 静态成员变量
  - 所有对象**共享**一份数据
  - 在编译阶段分配内存
  - 类内声明，类外初始化

- 静态成员函数
  - 所有对象**共享**同一个函数
  - 静态成员函数只能访问静态成员变量

```c
# include<iostream>
# include<string>
using namespace std;

class person
{
public:
	static void func()
	{
		a = 100;//静态成员函数可以访问静态成员变量
		//静态成员函数不能访问  非静态成员变量
		cout << "stactic void func调用" << endl;
    }
	static int a;//静态成员变量,类内声明
private:
	static void func2()
	{
		cout << "func2 的调用" << endl;
	}
	//类外访问不到私有的静态成员函数
};
int person::a = 0;//类外赋值，" :: "
void test01()
{
	//通过对象访问
	person p;
	p.func();
	//通过类名访问
	person::func();  //不用创建变量也能访问 ，" :: "
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

------

#### c++对象模型和this指针

##### 成员变量和成员函数分开存储



c++中，类的成员变量和成员函数**分开存储**

只有**非静态成员变量**才属于类的对象上



```c
# include<iostream>
# include<string>
using namespace std;

//成员变量 和成员函数 分开存储
class person
{
	int a;//没有加 static就是非静态成员变量
	static int b;//静态成员 不属于类的对象上
	void func() {}//非静态的成员函数
	static func2()
	{

	}//静态成员函数
};
static int b = 0;
void test01()
{
	person p;
	cout << sizeof(p) << endl;
	//c++编译器会给每个空对象分配一个字节空间，是为了区分空对象占内存的位置
	//每个空对象也应该有独一无二内存地址
}
void test02()
{
	person p;
	cout << sizeof(p) << endl;//非静态成员变量 属于类的对象上
}
int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```



##### this指针概念

**每一个非静态成员**只会诞生一份函数实例，也就是**多个同类型的对象**会共用一块代码

问题：这一块代码如何区分那个对象是调用自己的呢？



c++通过提供特殊的对象指针，this指针，解决上述问题

**this指针指向被调用的成员函数所属对象**



this指针是隐含每一个非静态成员函数内的一种指针

this指针不需要定义，直接使用即可



this指针的用途：

- 当形参和成员变量同名事物，可以用this指针来区分
- 在类的非静态成员函数中返回对象本身，可使用 return * this



###### 错误示范

```c
# include<iostream>
# include<string>
using namespace std;

//解决名称冲突

//返回对象本身使用*this
class person
{
public:
	person(int age)
	{
		age = age;//系统任务age是同一份
	}
	int age;
};
void test01()
{
	person p(18);
	cout << p.age << endl;
	
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```



###### 正解

```c
# include<iostream>
# include<string>
using namespace std;

//解决名称冲突

//返回对象本身使用*this
class person
{
public:
	person(int age)
	{
		//this指针指向被调用的成员函数 所属对象
		this -> age = age;
	}
	int age;
};
void test01()
{
	person p(18);
	cout << p.age << endl;
	
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

###### 对this的灵活运用

```c
# include<iostream>
# include<string>
using namespace std;

//解决名称冲突

//返回对象本身使用*this
class person
{
public:
	person(int age)
	{
		//this指针指向被调用的成员函数 所属对象
		this -> age = age;
	}
	void personaddage(person &p)
	{
		this->age += p.age;//把传进来的（引用）的p的age和本对象的age相加，并赋给自己
	}
	int age;
};
void test01()
{
	person p(18);
	cout << p.age << endl;
	
}
void test02()
{
	person p1(10);
	person p2(10);
	p2.personaddage(p1);
	cout << p2.age << endl;
}
int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

###### 让包含this的函数多次返回

原来的` p2.personaddage(p1)`

变成计算:`p2.personaddage(p1).personaaaage(p1).personaddage(p1)`

则需要有返回值

```c
# include<iostream>
# include<string>
using namespace std;

//解决名称冲突

//返回对象本身使用*this
class person
{
public:
	person(int age)
	{
		//this指针指向被调用的成员函数 所属对象
		this -> age = age;
	}
	person& personaddage(person& p)
	{//如果要返回本体，要通过引用的方式，返回值类型与类一致
		this->age += p.age;//把传进来的（引用）的p的age和本对象的age相加，并赋给自己
		return *this;
	}
	int age;
	return *this;//this是指向p2的指针，而*p2指向的就是p2这个对象本体
};
void test01()
{
	person p(18);
	cout << p.age << endl;
	
}
void test02()
{
	person p1(10);
	person p2(10);
	p2.personaddage(p1).personaddage(p1).personaddage(p1);
	cout << p2.age << endl;
}
int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

如果用引用的方式返回，它不会创建新的空间，直接返回`p2`

![](https://s4.ax1x.com/2021/12/13/oXTMb4.png)

![](../Snipaste_2021-12-13_18-13-39.png)

其中，`personaddage`就是包含this指针，被一直返回的函数





##### 空指针访问成员函数

c++中空指针也是可以调用成员函数的，但是也要注意有没有用到this指针



如果用到this指针，需要加以判断保证代码的健壮性

- 空指针（this指向的成员变量未赋值但是被调用），会引发程序崩溃，因此需要有一段判断

```c
# include<iostream>
# include<string>
using namespace std;

class person
{
public:
	void showclassname()
	{
		cout << "this is person class" << endl;
	}
	void showpersonage()
	{
		cout << "age= " << age << endl;
		if (this == NULL)
		{
			return;
		}//防止为空指针，发生崩溃
	}
	int age;
};
void test01()
{
	person* p = NULL;
	//p->showpersonage();
	p->showclassname();//会崩溃
	//因为每一个成员变量前面有隐藏的 "this->" ，即this指针，因为age''未赋值，则这是一个空指针
	//所有需要到这个showpersonage里面做一个判断
};
void test02()
{
	
}
int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```



##### const修饰成员函数

###### 基础

**前情** 

类中的每个成员函数内部都有一个 `this `指针

而`this`指针的本质是一个 **指针常量** `int * const`  （指针的指向不能修改）

**常函数**

- 成员函数**后加`const`**后，我们称这个函数是常函数
- 常函数内**不可以修改成员属性**
- 成员属性声明时加关键字 `mutable`后，在常函数中依旧可以修改



**常对象**

- 声明**对象前加`const`**称该对象为常对象
- 常对象**只能调用常函数**



###### 示例

- **常函数**

- 常函数内**不可以**修改成员属性

![](https://s4.ax1x.com/2021/12/13/oXTsPI.png)

- this指针指向的是对象

![](https://s4.ax1x.com/2021/12/13/oX7pJ1.png)

如图，如果将this赋值为 空 ，那么系统会报错，因为this 是指向对象 p的指针



**this指针不能修改指向，**但是指针指向的值（比如p，p是类，内部有a),可以修改自己内部的成员属性



如果想让this指向的对象修改不了内部成员变量的值，可以加在函数（小括号）后面

![](https://s4.ax1x.com/2021/12/13/oX7kLD.png)



如果对于某些特殊的变量，想让个别的数能被修改，可以使用`mutable`

![](https://s4.ax1x.com/2021/12/13/oX7GwQ.png)



```c
# include<iostream>
# include<string>
using namespace std;
//常函数，常对象


class person
{
public:
	
	void showperson() const
	{
		this->b=20;
	}
	int a;
	mutable int b;
};
void test01()
{
	person p;
	p.showperson();
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```



- **常对象**

![](https://s4.ax1x.com/2021/12/13/oX7NYn.png)



常对象也不能被修改，同常函数，可以在想被修改的成员变量前加 `mutable`



**常对象只能调用常函数**

![](https://s4.ax1x.com/2021/12/13/oX70yT.png)

------



#### 友元

##### 基础

在程序里，有些私有属性，也想让类外特殊的一些函数或者类进行访问，就需要用到友元的技术

友元的目的就是让一个函数或者类，访问另一个类中的私有成员

友元的关键字为 **friend**



**友元的三种实现**

- 全局函数做友元
- 类做友元
- 成员函数做友元



##### 全局函数做友元

![](https://s4.ax1x.com/2021/12/13/oX7ck9.png)



- 只需要把该想要访问私有成员的函数声明，放在类内的第一行，并且在前面加上 **“friend” **即可



##### 类做友元

同理，copy声明到类内第一行，并且在前面加 **“friend”** 即可

本例还要拓展其他知识

```c
# include<iostream>
# include<string>
using namespace std;

class building;//声明之后会定义一个叫 building 的类
class goodguy
{
public:
	void Goodguy();
	void visit();//参观函数，访问building中的属性
	building* build;
};


class building
{
friend class goodguy();
public:
	void Building();
	string sittingroom;
private:
	string bedroom;
};
//类外定义成员函数
void goodguy::Goodguy()
{
	build = new building;//在堆区创建一个对象，让building * 指向这个对象
}
void goodguy::visit()
{
	cout << "好基友在访问： " << build->sittingroom << endl;
}
//类外定义成员函数
void building::Building()
{
	sittingroom = "客厅";
	bedroom = "卧室";
}


void test1()
{
	goodguy gg;
	gg.visit();
}
int main()
{
	test1();
	system("pause");
	return 0;
}
```

- 以上友细节问题以及运行时报错。
- 细节：类内函数在类外定义的时候，要声明来自那个类

`数据类型 类名 :: 函数名 () {} `

- 

  

##### 成员函数做友元

类似的，其他类的成员函数想要访问某一个类中的私有成员，比如此例子中，`goodguy类`中的visit函数想要访问 `Building类`中的私有成员`bedroom` 则需要在`Building类`中  说明  

 `friend goodguy:: visit();`,代表`gooodguy`所属的visit函数是友元



```c
# include<iostream>
# include<string>
using namespace std;

class Building;
class goodguy
{
public: 
    goodguy();//构造函数，自动执行一次
	void visit1();//让visit1函数可以访问Building中的私有成员
	void visit2();//让visiy2函数不可以访问Building中的私有成员
	Building* building;//和goodguy()这个构造函数结合相当于，building指向一块Building的空间
};

class Building
{
	//goodguy类下的成员函数想要访问此类中 的私有成员
friend void goodguy::visit1();
public:
	Building();
public:
	string sittingroom;
private:
	string bedroom;
};
Building::Building()
{
	sittingroom = "客厅";
	bedroom = "卧室";
}
goodguy::goodguy()
{
	building = new Building;//goodguy内部维护着Building* 的指针，在堆区开辟一块空间
}
void goodguy:: visit1()//访问函数的内容在类外定义
{
	cout << "visit1函数正在访问" << building->sittingroom << endl;
	cout << "visit1函数正在访问" << building->bedroom << endl;
}
void goodguy:: visit2()//访问函数的内容在类外定义
{
	cout << "visit2函数正在访问" << building->sittingroom << endl;
	//cout << "visit2函数正在访问" << building->bedroom << endl;
}
void test1()
{
	goodguy gg;
	gg.visit1();
	gg.visit2();
}
int main()
{
	test1();
	system("pause");
	return 0;
}
```

------



#### 运算符重载:call_me_hand:



运算符重载概念：对**已有的运算符**重新进行定义，赋予其另一种功能，以适应不同的数据类型



##### 加号运算符重载

作用：实现 2 个**自定义数据类型**相加的运算



对于内置的数据类型，编译器知道如何运算



但是自定义类，比如 人，卧室，等类进行运算，编译器不知道怎么运算，这需要我们进行定义实现



**通过成员函数实现+号重载：**

![](https://s4.ax1x.com/2021/12/14/ojGDJK.png)

![](https://s4.ax1x.com/2021/12/14/ojGbLj.png)



**通过全局函数实现+号重载：**

![](https://s4.ax1x.com/2021/12/14/ojJvBd.png)



**本质：**

成员函数：`person p3 =p1.operator+ (p2)`

全局函数：`person p3 =operator+(p1,p2)`



**示例：**

```c
# include<iostream>
# include<string>
using namespace std;

//通过成员函数实现重载+号

//全局函数实现重载+号
class person
{
public: 
	//用成员函数实现重载
	//person operator+(person& p)
	//{
	//	person temp;
	//	temp.a = this->a + p.a;
	//	temp.b = this->b + p.b;
	//	return temp;
	//}
	int a;
	int b;
};

//通过全局函数实现+号重载
person operator+ (person& p1, person& p2)
{
	person temp;
	temp.a = p1.a + p2.a;
	temp.b = p1.b + p2.b;
	return temp;
}
void test1()
{
	person p;
	p.a = 10;
	p.b = 20;
	person p2;
	p2.a = 30;
	p2.b = 10;

	person p3 = p + p2;//注释掉成员函数，利用全局函数实现这个功能
	cout << p3.a <<"  " << p3.b << endl;
}
int main()
{
	test1();
	system("pause");
	return 0;
}
```



还有函数重载，比如上例子，`person p3 =p1+10;`会报错，因为`int`和`person`是两种数据类型



这个时候可以定义一个函数

```c
person operator+ (person &p1,int nun)
{
    person temp;
    temp->a=p1.a+num;
    temp->b=p1.b+num;
    return temp;
}
```

**总结**

> 对于内置数据类型的表达式的运算符是不可能改变的
>
> 不要滥用运算符重载



##### 左移运算符的重载

作用：可以输出自定义数据类型

**代码示例：**

```c
# include<iostream>
# include<string>
using namespace std;

class person
{
	friend ostream& operator<<(ostream& cout, person& p);
public:
	person(int a, int b)
	{
		a = a;
		b = b;
	}
private: 
	//左移运算符重载
	//简化形式就是 p<<cout,而我们想要的是 cout<<p,不符合
	//所以我们一般不会利用成员函数重载<<运算符，因为无法实现 cout 在左侧
	//void operator<< (cout)
	int a;
	int b;
};

//通过全局函数实现<<号重载
ostream&  operator<<(ostream &cout, person &p)
{
	cout << p.a << " " << p.b << endl;
	return cout;//则后面的输出流可以无限追加
}
void test1()
{
	person p(10,10);//初始化的同时，调用构造函数实现对a,b赋初值
	//p.a = 10;//a,b是私有成员，不能类外赋值，那就可以使用构造函数赋初值
	//p.b = 20;
	cout << p << endl; 
	//返回值为 void 则 endl报错
	//ostream类型必须是引用类型，所以返回值必须是引用，要把返回值和参数都设置为一种类型
}
int main()
{
	test1();
	system("pause");
	return 0;
}
```



**细节点拨**



- 要重载<<,只能使用全局函数实现，且如果要访问私有成员，还要利用友元

 ![](https://s4.ax1x.com/2021/12/15/ozDi6A.png)



- 如果该重载函数返回值类型为void，可以发现，调用的时候不能在后面加`<<endl;`,则需要把返回值类型设置为 `ostream& `,`return cout`

  ,实现无限输出追加

![](https://s4.ax1x.com/2021/12/15/ozD800.png)



- 私有成员不能在类外部赋值，可以构造函数，让初始化对象的同时对私有成员赋值

![](https://s4.ax1x.com/2021/12/15/ozDghD.png)





##### 递增运算符重载

作用：通过重载递增运算符，实现自己的整型数据



```c
# include<iostream>
# include<string>
using namespace std;

class person
{
	friend ostream& operator<<(ostream& cout, person& p);
	friend ostream& operator<<(ostream& cout, person p);
public:
	person()
	{
		a = 0;
	}
	//前置++一定做引用返回
	person& operator++()//返回的是一个引用，因为如果不是引用，++a之后a的值也被赋值为a+1，而不是原来的数字
	{//返回引用是为了一直第一个数据进行递增操作比如，++（++a）
		a++;
		return *this;//需要对自身做一个返回
	}
	//后置++一定做值返回
	person operator++(int)
		//int代表占位参数，可以用于区分前置后置递增
	{
		//先记录当前结果
		person temp = *this;
		//后递增
		a++;
		//最后记录结果做返回
		return temp;
	}
	person(int A)
	{
		a = A;
	}
private: 
	//重载递增运算符
	int a;
};
ostream& operator<<(ostream& cout, person& p)
{
	cout << p.a;
	return cout;
}
ostream& operator<<(ostream& cout, person p)
{
	cout << p.a;
	return cout;# include<iostream>
# include<string>
using namespace std;

class person
{
	//friend ostream& operator<<(ostream& cout, person& p);
	friend ostream& operator<<(ostream& cout, person p);
public:
	person()
	{
		a = 0;
	}
	//前置++一定做引用返回
	person& operator++()//返回的是一个引用，因为如果不是引用，++a之后a的值也被赋值为a+1，而不是原来的数字
	{//返回引用是为了一直第一个数据进行递增操作比如，++（++a）
		a++;
		return *this;//需要对自身做一个返回
	}
	//后置++一定做值返回
	person operator++(int)
		//int代表占位参数，可以用于区分前置后置递增
	{
		//先记录当前结果
		person temp = *this;
		//后递增
		a++;
		//最后记录结果做返回
		return temp;
	}
	person(int A)
	{
		a = A;
	}
private: 
	//重载递增运算符
	int a;
};
ostream& operator<<(ostream& cout, person& p)
{
	cout << p.a;
	return cout;
}
ostream& operator<<(ostream& cout, person p)
{
	cout << p.a;
	return cout;
}
void test1()
{
	person p(20);
	//cout << p++ ;
	cout <<++p << endl;
	cout << p++ << endl;
	cout << p << endl;
}
int main()
{
	test1();
	system("pause");
	return 0;
}
}
void test1()
{
	person p(20);
	//cout << p++ ;
	cout << p++ << endl;
	cout << ++p << endl;
}
int main()
{
	test1();
	system("pause");
	return 0;
}
```



- 发现：越到后面，与前面的关联更大，递增运算符重载之前，需要左移运算符重载

![](https://s6.jpg.cm/2021/12/15/LVfNdh.png)

需要重新再定义一个左移运算符，但是实践出现，返回值不为`ostream&`，无法在后置++后无限输出流。



- 解决，实际上，在重载<<的时候，第二个参数就是需要++的那个数的返回值类型，前置++第二个参数返回引用；后置++第二个参数返回值；

- 不过有新的问题，同时定义多个重载类型会报错:woman_playing_handball:



##### 赋值运算符重载

c++编译器至少给一个类添加4个函数

1. 默认构造函数（无参，函数体为空）

2. 默认构析函数（无参，函数体为空）

3. 默认拷贝函数，对属性进行值拷贝

4. 赋值运算符 operator=，对属性进行值拷贝

   

   

   （小烦，这里有太多细节，感觉插在这里不好，我先把基础的嚼完再回来，等我~）

   ------



#### 继承

##### 基础语法

继承是面向对象三大特性之一

定义类的时候，下级别的成员除了有上一级的共性，还有自己的 特性

**好处**：减少重复代码

**语法****：class 子类：public 父类 {   }**

子类又叫派生类，父类又叫基类



```c
# include<iostream>
# include<string>
using namespace std;

class basepage
{
public:
	void header()
	{
		cout << "首页" << endl;
	}
	void footer()
	{
		cout << "帮助中心" << endl;
	}
	void content()
	{
		cout << "ja" << endl;
	}
};
//java
class java :public basepage//公共部分的继承
{
	void content()
	{
		cout << "java" << endl;
	}
};
//python
class python :public basepage
{
	void content()
	{
		cout << "python" << endl;
	}
};
int main()
{
	system("pause");
	return 0;
}
```



##### 继承方式

继承语法：`class子类 ： 继承方式 父类 `

继承方式有3种：

- 公共继承
- 保护继承
- 私有继承



class a :**public** base

- 私有成员不可访问，公共成员和保护成员依旧分别为公共成员和保护成员



class b :**protected** base

- 私有成员不可访问，公共成员和保护成员都变成保护成员、



class c : **private** base

- 私有成员都 变成私有成员





##### 继承中的对象模型

**问题**：从父类继承过来的成员，哪些属于子类对象？



在父类中所有**非静态成员属性**都会被子类继承下去，

- 比如包括父类中的三种属性对应的三个变量int a，int b ，int c，子类中有一个int d，则子类一共开辟的空间为`4*sizeof（int）`=16



- 父类中私有成员属性 是被编译器隐藏了，因此访问不到，但是确实被继承下去了



```c
# include<iostream>
# include<string>
using namespace std;
//继承中的对象模型
class base
{
public:
	int a;
protected:
	int b;
private:
	int c;
};
class son :public base//公共部分的继承
{
public:
	int d;
};
//python
void test()
{
	cout << sizeof(son) << endl;
	//在父类中所有非静态成员属性都会被子类继承下去
	//父类中私有成员属性 是被编译器隐藏了，因此访问不到，但是确实被继承下去了
}
int main()
{
	test();
	system("pause");
	return 0;
}
```



##### 继承中构造和构析顺序



子类继承父类后，当创建子类对象，也会调用父类的构造函数



**问题：**父类和子类的构造和构析函数 是谁先谁后？

结论：继承中的构造和析构的顺序，先构造父类再构造子类，先析构儿子，再析构父亲



```c
# include<iostream>
# include<string>
using namespace std;
//继承中的构造和析构的顺序
class base
{
public:
	base()
	{
		cout << "base的构造函数" << endl;
	}
	~base()
	{
		cout << "base的析构函数" << endl;
	}
};
class son :public base//公共部分的继承
{
public:
	son()
	{
		cout << "son的构造函数" << endl;
	}
	~son()
	{
		cout << "son的构析函数" << endl;
	}
};
void test()
{
	son s;
}
int main()
{
	test();
	system("pause");
	return 0;
}
```



![](../Snipaste_2021-12-16_08-43-00.png)



##### 继承同名成员处理方法

问题：当父类与子类中出现同名的成员，如何通过子类对象，访问到子类或父类中同名的数据呢



- 访问子类同名成员，直接访问即可
- 访问父类同名成员，需要加作用域



如果子类中出现和父类同名的成员函数，父类中的同名函数会被隐藏掉，要想访问**必须加作用域**

```c
# include<iostream>
# include<string>
using namespace std;
//继承中同名成员的处理方法
class base
{
public:
	int a;
	base()
	{
		a = 100;
	}
	void func()
	{
		cout << "base" << endl;
	}
};
class son :public base//公共部分的继承
{
public:
	int a;//和父类的成员同名
	son()
	{
		a = 200;
	}
	void func()
	{
		cout << "son" << endl;
	}
};
//如果子类中出现和父类同名的成员函数，父类中的同名函数会被系统隐藏掉，要想访问必须加作用域
void test()
{
	son s;
	//同名成员属性的处理方式
	cout << s.a << endl;//访问子类自身直接访问
	cout << s.base::a << endl;//在同名成员属性前，加上父类作用域，就是访问父类的成员
	//同名成员函数的处理方式
	 s.func();
	 s.base::func();
}
int main()
{
	test();
	system("pause");
	return 0;
}
```



##### 继承中同名静态成员的处理方法

问题：继承中同名的静态成员在子类对象上如何进行访问？



静态成员和非静态成员出现同名，处理方式一致



- 访问子类同名成员，直接访问即可
- 访问**父类同名成员，需要加作用域**



```c
# include<iostream>
# include<string>
using namespace std;
//继承中同名静态成员的处理方法

class base
{
public:
	static int a;//静态成员，类内声明，类外赋值
};
int base::a = 100;//类外声明


class son :public base//公共部分的继承
{
public:
	static int a;
};
int son::a = 200;//类外声明


void test()
{
	//访问静态成员的两种方式，通过对象访问
	son s;
	cout << s.a << endl;//访问子类自身直接访问
	cout << s.base::a << endl;//在同名成员属性前，加上父类作用域，就是访问父类的成员

	//通过类名访问
	cout << son::a << endl;
	cout << base::a << endl;
	//上面2种代表通过类名的方式来访问
	cout << son::base::a << endl;
	//以上两个双冒号，代表访问父类作用域下
}
//同名的静态函数也是如此
int main()
{
	test();
	system("pause");
	return 0;
}
```



##### 多继承语法



c++允许一个类继承多个类



语法：`class 子类 : 继承方式 父类1，继承方式 父类2...`



多继承可能引发父类中有同名成员出现，需要**加作用域区分**



c++实际开发中**不建议**使用多继承

```c
# include<iostream>
# include<string>
using namespace std;
//继承中多继承语法

class base1
{
public:
	base1()
	{
		a = 10;
	}
	int a;

};
class base2
{
public:
	base2()
	{
		a = 60;
	}
	int a;

};

class son :public base1, public base2//公共部分的继承
{
public:
	son()
	{
			c = 30;
			d = 40;
}
	int c;
	int d;
};



void test()
{
	son s;
	cout << sizeof(s) << endl;
	cout <<s.base1::a << endl;
	cout << s.base2::a << endl;
}
int main()
{
	test();
	system("pause");
	return 0;
}
```



##### 菱形继承

菱形继承**概念：**

- 两个派生类（子类）继承一个基类（父类）
- 又有某个类同时继承两个派生类
- 这种继承方式被称为菱形继承，或者钻石继承



典型的菱形继承**案例：**

​              羊     

动物->             ->羊驼

​            骆驼

菱形继承的问题：

1. 羊继承了动物的数据，骆驼同样继承了动物的数据，当羊驼使用数据的时候，就会产生**二义性**
2. 羊驼继承来自动物的数据继承了2份，但是事实上继承1份就行

**解决方法**：使用虚继承，即在子类继承的public前加 virtual--->

`class son :virtual public father`



```c++
# include<iostream>
# include<string>
using namespace std;
class animal {
public:
	int age;

};
//利用虚继承可以解决菱形继承的问题
//继承之前加上 关键字 virtual 变为虚继承，animal变为虚基类
//数据变为一份，因为内部有一个vbptr指针，指向vbtable
class sheep :virtual public animal
{
public:
	int a;

};
class tuo:virtual public animal
{
public:
	int a;

};

class sheeptuo :public sheep, public tuo//公共部分的继承
{
public:
	int d;
};
```

------



#### 多态

##### 基础

**多态分为2类**

- 静态多态：函数重载和运算符重载属于静态多态，复用函数名
- 动态多态：派生类和虚函数实现运行时多态



**静态多态和动态多态区别：**

- 静态多态的函数地址早绑定，编译阶段确定函数地址
- 动态多态的函数地址晚绑定，运行阶段确定函数地址





**动态多态的满足条件：**

1. 有继承关系
2. 子类要**重写**（返回值类型，函数名，形参列表中所有内容都相同）父类的**虚函数**（父类改同名函数定义前加virtual）



**动态多态的使用：**

父类的指针或者引用 指向子类对象

`dospeak(animal & animal)`-----> `dospeak(cat)`

(指针指向子类对象)

**案例：**

- 当父类子类中有同名函数

```c++
# include<iostream>
# include<string>
using namespace std;
class animal {
public:
	void speak()
	{
		cout << "动物在说话" << endl;
	}
};

class cat : public animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}

};
class tuo:virtual public animal
{
public:
	int a;

};

void dospeak(animal &animal)//animal&animal =cat
{
	animal.speak();
}
void test()
{
	cat ca;
	ca.speak();//函数调用
	
}
int main()
{
	cat ca;
	dospeak(ca);
	system("pause");
	return 0;
}
```



如果初始化子类，引用子类调用同名函数，结果输出父类的函数内容

原因是：地址早绑定，在**编译阶段**就确定了函数地址



- 如果想要执行子类的函数内容，那么就不能让这个地址早绑定，在**运行阶段**进行绑定，地址晚绑。

- 方法：在父类中对该同名函数定义数据类型前，加virtual

​            `virtual void speak()`

```c++
# include<iostream>
# include<string>
using namespace std;
class animal {
public:
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};

class cat : public animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}

};
class tuo:virtual public animal
{
public:
	int a;

};

void dospeak(animal &animal)//animal&animal =cat
{
	animal.speak();
}
void test()
{
	cat ca;
	ca.speak();//函数调用
	
}
int main()
{
	cat ca;
	dospeak(ca);
	system("pause");
	return 0;
}
```



##### 多态的基本概念

（基本知识在画图工具，等一下重新看一遍做笔记）

在父类该同名函数前加 virtual 就使得 `vbftr`指向的`vbtable`被子类的函数指针覆盖

（**开发人员命令提示符）**



##### 多态案例1---计算器类

案例描述：

分别利用普通写法和多态技术，设计实现两个操作进行运行的计算器类



多态的优点：

- 代码组织结构清晰
- 可读性强
- 利用前期和后期扩展加以维护



案例：

- 传统写法

```c++
# include<iostream>
# include<string>
using namespace std;
//用普通写法和多态实现计算器
class calculator {
public:
	int sum(string oper)
	{
		if (oper == "+")
		{
			return num1 + num2;
		}

		else if (oper == "-")
		{
			return num1 - num2;
		}
		else if (oper == "*")
		{
			return num1 *num2;
		}
		
	}
	int num1;
	int num2;
};
void test()
{
//创建一个计算器的对象
	calculator c;
	c.num1 = 10;
	c.num2 = 10;
	cout << c.sum("+") << endl;
	
}
int main()
{
	test();
	system("pause");
	return 0;
}
```

- 如果要拓展新的功能，需要修改源码

- 在实际开发中 提倡 **开闭原则**

- 开闭原则：对扩展进行开发，对修改进行关闭





- 多态写法

```c+=
# include<iostream>
# include<string>
using namespace std;
//利用多态实现计算器

//实现计算器的抽象类

class abstractcalculator
{
public:
	virtual int getresult()//子类重写父类虚函数
	{
		return 0;
	}
	int num1;
	int num2;
};

class addcalculator : public abstractcalculator
{
public:
	int getresult()
	{
		return num1 + num2;
	}
};

class subcalculator : public abstractcalculator
{
public:
	int getresult()
	{
		return num1 - num2;
	}
};


class mulcalculator : public abstractcalculator
{
public:
	int getresult()
	{
		return num1 * num2;
	}
};
void test()
{
	//多态使用条件：
	//父类指针或者引用指向子类对象

	//加法运算
	abstractcalculator* c = new addcalculator;//开辟空间，让父类指针指向子类对象，创建在堆区
	c->num1 = 10;
	c->num2 = 10;
	//c指向的是加法类
	cout << c->getresult() << endl;
	
	delete c;//堆区数据要手动释放

	c = new subcalculator;
	cout << c->getresult() << endl;

	delete c;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



##### 纯虚函数和抽象类



在多态中，通常父类中的虚构函数的实现是毫无意义的，主要都是**调用子类重写**的内容



因此可以将虚函数改为纯虚函数



**纯虚函数的语法：**`virtual 返回值类型 函数名 （参数列表） =0;`（就是在虚函数的基础上写 =0；）

 

当类中有了纯虚函数，这个类也称为**抽象类**



抽象类特点：

- 无法实例化对象
- **子类**必须**重写抽象类中的纯虚函数**，否则也属于抽象类



多态的**使用条件**是父类的指针或者引用指向子类的对象



```c++
# include<iostream>
# include<string>
using namespace std;
class base
{
public:
	//纯虚函数
	//只要有一个纯虚函数，这个类称为抽象类
	//抽象类特点：
	//1,无法实例化对象
	//抽象类的子类，必须要重写父类中的虚函数，否则也属于抽象类
	virtual void func() = 0;
};

class son :public base
{
	//重写父类中的虚函数
public:
	virtual void func()
	{
		cout << "func" << endl;
	}
};
void test()
{
	son s;
	//多态的使用条件是，父类的指针后引用指向子类对象
	base* ba = new son;
	ba->func();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

![](https://s6.jpg.cm/2021/12/17/LAS1GS.png)



##### 多态案例2--制作饮品

制作饮品的大致流程为：煮水->冲泡->导入杯中->加入辅料



利用**多态技术实现**本案例，提供**抽象制作饮品基类**，提供制作咖啡和茶叶

```c++
# include<iostream>
# include<string>
using namespace std;
//多态案例2 制作饮品
class abstractdrinking
{
public:
	//煮水
	virtual void boil() = 0;

	//冲泡
	virtual void brew() = 0;

	//倒入杯中
	virtual void pour() = 0;

	//倒入其他
	virtual void otherthing() = 0;

	void makedrink()
	{
		boil();
		brew();
		pour();
		otherthing();
	}
};

class son :public abstractdrinking
{

	virtual void boil()
	{
		cout << "1" << endl;
	}
	virtual void brew()
	{
		cout << "2" << endl;
	}
	virtual void pour()
	{
		cout << "3" << endl;
	}
	virtual void otherthing()
	{
		cout << "4" << endl;
	}
};
//制作茶叶
class tea :public abstractdrinking
{
	virtual void boil()
	{
		cout << "5" << endl;
	}
	virtual void brew()
	{
		cout << "6" << endl;
	}
	virtual void pour()
	{
		cout << "7" << endl;
	}
	virtual void otherthing()
	{
		cout << "8" << endl;
	}
};

void dowork(abstractdrinking* a)
{
	a->makedrink();
	delete a;
}
void test()
{
	dowork(new tea);//这里的tea是子类的类型说明
}
int main()
{
	test();
	system("pause");
	return 0;
}
```







##### 虚析构和纯虚析构



多态使用时，如果子类中**有属性开辟到堆区**，那么父类指针在释放时无法调用子类中的析构代码



解决方法：将父类中的析构函数改为虚析构或者纯虚析构



虚析构和纯虚析构共性:

- 可以解决父类指针释放子类对象
- 都需要有具体的函数实现

虚析构和纯虚析构的区别：

- 如果是纯虚析构，该类属于抽象类，无法实例化对象





虚析构语法：

`virtual ~类名() {}`

纯虚析构语法:

`virtual ~类名 ()=0`



```c++
# include<iostream>
# include<string>
using namespace std;
//多态案例2 制作饮品
class animal
{
public:
	animal()
	{
		cout << "animal的构造函数调用" << endl;
	}
	~animal()
	{
		cout << "animal的析构函数调用" << endl;
	}
	virtual void speak() = 0;//纯虚函数
};

class cat:public animal
{
public:
	cat(string Name)
	{
		cout << "cat的构造函数调用" << endl;
		name = new string(Name);//让指针指向堆区
	}
	string* name;//让它指向堆区



	virtual void speak()
	{
		cout << "catttter" << endl;
	}
	~cat()//析构函数内清空内存
	{
		cout << "cat的析构函数调用" << endl;
		delete name;
		name = NULL; //置空是为了避免野指针
	}
};

void test()
{
	animal* an = new cat ("an");
	an->speak();
	delete an;
    //delete 父类的指针，不会走子类的析构代码
}
int main()
{
	test();
	system("pause");
	return 0;
}
```



以上例子**子类的析构函数没有被调用**

![](https://s4.ax1x.com/2021/12/17/TAFiOH.png)



说明没有走到 `~cat()` 内的代码，即cat析构函数内部的释放没有完成，会造成内存泄漏



- 原因： delete 父类的指针，不会走子类的析构函数

- 子类除了有自己的析构还有继承的析构，用父类指针默认调用父类的析构



利用**虚析构**可以解决这个问题



```c++
# include<iostream>
# include<string>
using namespace std;
//多态案例2 制作饮品
class animal
{
public:
	animal()
	{
		cout << "animal的构造函数调用" << endl;
	}
	virtual ~animal() = 0;//纯虚析构函数，到外部实现，这是声明
	
	virtual void speak() = 0;//纯虚函数
};
animal::~animal()//表明是animal下面的纯虚析构函数声明
{
	cout << "animal的析构函数调用" << endl;
}
//有了纯虚析构之后，这个类也属于抽象类，无法实例化对象
class cat:public animal
{
public:
	cat(string Name)
	{
		cout << "cat的构造函数调用" << endl;
		name = new string(Name);//让指针指向堆区
	}
	string* name;//让它指向堆区



	virtual void speak()
	{
		cout << "catttter" << endl;
	}
	~cat()//析构函数内清空内存
	{
		cout << "cat的析构函数调用" << endl;
		delete name;
		name = NULL; //置空是为了避免野指针
	}
};

void test()
{
	animal* an = new cat ("an");
	an->speak();
	delete an;
}
int main()
{
	test();
	system("pause");
	return 0;
}
```



- 总结：

1. 虚析构或者纯虚析构就是用来解决**通过父类指针释放对象**
2. 如果子类中没有堆区数据，可以不写虚析构或纯虚析构
3. 拥有纯虚析构函数的类也属于抽象类





##### 多态案例3--电脑组装



案例描述：

![](https://s4.ax1x.com/2021/12/19/TZ8hgU.png)



- 基本的类，比如每一台电脑都需要的零件 `cpu `，显卡，内存条等用虚构函数写，之后调用
- 同时复习上节课知识：子类要释放在堆区开辟的空间，需要通过父类的构析函数对其进行释放
- 类的定义和开辟空间，释放空间都需要手动

```c++
# include<iostream>
# include<string>
using namespace std;
//抽象不同零件的类
//抽象cpu类
class cpu
{
public:
	//抽象的计算函数
	virtual void calculate() = 0;

};
//抽象显卡类
class videocard
{
public:
	//抽象的计算函数
	virtual void display() = 0;

};
//抽象存储类
class memory
{
public:
	//抽象的存储函数
	virtual void storage() = 0;

};

//电脑类
class computer
{
public:
	computer(cpu* cpu, videocard* v, memory* mem)
	{
		cp = cpu;
		vc = v;
		me = mem;
	}
	void work()
	{
		//让零件工作起来，调用接口
		cp->calculate();
		vc->display();
		me->storage();
	}
	~computer()
	{
		delete cp;
		cp = NULL;
		delete vc;
		vc = NULL;
		delete me;
		me = NULL;
	}
private:
	cpu* cp;//cpu的零件指针
	videocard* vc; //显卡零件指针
	memory* me;//内存条零件指针
};

//具体厂商
class intelcpu :public cpu
{
public:
	virtual void calculate()
	{
		cout << "intel的cpu" << endl;
	}
};
class intelvideocard :public videocard
{
public:
	virtual void display()
	{
		cout << "intel的videocard" << endl;
	}
};
class intelmem :public memory
{
public:
	virtual void storage()
	{
		cout << "intel的memory" << endl;
	}
};


class lenovolcpu :public cpu
{
public:
	virtual void calculate()
	{
		cout << "lenovo的cpu" << endl;
	}
};
class lenovovideocard :public videocard
{
public:
	virtual void display()
	{
		cout << "lenovo的videocard" << endl;
	}
};
class lenovomem :public memory
{
public:
	virtual void storage()
	{
		cout << "lenovo的memory" << endl;
	}
};

void test()
{
	//第一台电脑的零件
	cpu* incpu = new intelcpu;//父类cpu的指针指向堆区开辟的子类
	videocard* incard = new intelvideocard;
	memory* memory = new intelmem;
	//创建第一台电脑
	computer* com = new computer(incpu, incard, memory);
	com->work();
	delete com;
	//在父类的析构函数中释放子类开辟的堆区空间（此处是电脑零件）

	//创建第二台电脑
	computer* com2 = new computer(new lenovolcpu, new lenovovideocard, new lenovomem);
	com2->work();
	delete com2;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

------



## 文件操作

程序运行时产生的数据都属于临时数据，程序一旦运行结束就会被释放

通过文件可以将**数据持久化**

c++中对文件操作需要包含**头文件 <fstream>**





文件类型分为两种：

- 文本文件： 文件以文本的 **ASCII码**形式存储在计算机中
- 二进制文件：文件以文本的**二进制**形式存储在计算机中，用户一般不能直接读懂它们



操作文件的三大类：

1. `ofstream`:写操作
2. `ifstream`:读操作
3. `fstream`:读写操作



### 文本文件

#### 写文件

 **步骤：**

1. 包含头文件   `#include< fstream>`
2. 创建流对象` ofstream ofs;`
3. 打开文件`ofs.open`("文件路径"，打开方式)
4. 写数据`ofs<<"写入的数据"`
5. 关闭文件`ofs.close();`



**文件打开方式**

| 打开方式      | 解释                       |
| :------------ | -------------------------- |
| `ios::in`     | 为读文件而打开文件         |
| `ios::out`    | 为写文件而打开文件         |
| `ios::ate`    | 初始位置：文件尾           |
| `ios::app`    | 追加方式写文件             |
| `ios::trunc`  | 如果文件存在先删除，再创建 |
| `ios::binary` | 二进制方式                 |



**注意**：文件打开方式可以配合使用，利用 | 操作符

**例如：**：用二进制方式写文件 

`ios::binary  | ios::out`



```c++
# include<iostream>
# include<string>
# include <fstream>
using namespace std;
//文本文件 写文件
void test()
{
	//1，包含头文件 fstream
	//2,创建一个流对象
	ofstream ofs;
	//3，指定打开方式
	ofs.open("test.txt", ios::out);

	//4，写内容
	ofs << "姓名：张三" << endl;
	ofs << "性别：男" << endl;
	ofs << "年龄：18" << endl;

	//5，关闭文件
	ofs.close();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



- 打开文件提示

![](https://s4.ax1x.com/2021/12/19/TZDP9H.png)

- 创建在代码文件的路径下

![](https://s4.ax1x.com/2021/12/19/TZslmq.png)

- **总结：**

1. 文件操作必须包含头文件` fstream`
2. 读文件可以利用`ofstream`,或者`fstream`类
3. 打开文件时候需要指定操作文件的路径，以及打开方式
4. 利用`<<`可以向文件中写数据
5. 操作完毕，要关闭文件



#### 读文件

读文件和写文件步骤类似，但是读取方式相对于比较多



读文件步骤如下：

1. 包含头文件  `#include<fstream>`
2. 创建流对象`ifstream ifs;`
3. 打开文件并判断文件是否成功打开` ifs.open("文件路径"，打开方式)`
4. 读数据‘ 四种方式读取
5. 关闭文件`ifs.close();`



**示例：**

```c++
# include<iostream>
# include<string>
# include <fstream>
using namespace std;
//文本文件 读文件
void test()
{
	//1，包含头文件 fstream
	//2,创建一个流对象
	ifstream ifs;
	//3，指定文件并且判断是否成功打开
	ifs.open("test.txt", ios::in);
	if (!ifs.is_open())
	{
		cout << "文件打开失败了" << endl;
		return;
	}
	//4，读数据
	//第一种
	//char buf[1024] = { 0 };
	//while (ifs>>buf)//读到头就会返回0
	//{
	//	cout << buf << endl;
//}
	
	//第二种
	//while (ifs.getline(buf, sizeof(buf)))//geiine的参数有2个，一个是文件，一个是文件大小
	//{
	//	cout << buf<< endl;
	//}

	//第三种
	//string buf;
	//while (getline(ifs, buf))//参数有2个，输出流和文件
	//{
	//	cout << buf << endl;
	//	
	//}
	
	//第四种
	char c;
	while ((c = ifs.get()) != EOF)//get每一次只读一个字符
	{
		cout << c ;
	}
	//5，关闭文件
	ifs.close();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



**总结：**

- 读文件可以利用 `ifstream`，或者` fstream`
- 利用`is_open`函数可以判断文件是否打开成功
- `close`关闭文件
- 四种打开方式

| char `buf` [1024]={0} | while(ifs>>`buf`){}                   |
| --------------------- | ------------------------------------- |
| char `buf`[1024]={0}  | `while(ifs.getline(buf,sizeof(buf)))` |
| string `buf`          | `while(getline(ifs,buf))`             |
| char c                | `while((c=ifs.get())!=EOF)`           |



### 二进制文件

以二进制的方式对文件进行读写操作

打开方式要指定为 `ios::binary`



可以操作不单单是内置的数据类型，还有结构体，类等其他自定义的数据类型



#### 写文件

二进制方式写文件主要利用流对象调用 **成员函数write**

函数原型：

`ostream& write(const char *buffer ,int len);`

参数解释：

字符指针buffer指向内存中一段存储空间，`len`是读写的字节数



示例：

```c++
# include<iostream>
# include<string>
# include <fstream>
using namespace std;
//二进制文件 写文件
class person
{
public:
	char name[64];//string本身是一个类，尽量不要读取自定义的类型中有string，会吧类写进去
	//char是c语言的字符串
	int age;

};
void test()
{
	//1,包含头文件
	//2，创建流对象
	ofstream ofs;
	//3,打开文件
	ofs.open("person.tex", ios::out | ios::binary);
	//4,写文件
	person p = { "ahelly",20 };
	ofs.write((const char*)&p, sizeof(person));
	//5,关闭文件
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



#### 读文件

二进制读文件主要利用流对象调用成员函数 read

函数原型:`istream& read(char* buffer,int len);`

参数解释：字符指针buffer指向内存中一块存储空间，len是读写的字节数



示例：

```c++
# include<iostream>
# include<string>
# include <fstream>
using namespace std;
//二进制文件 读文件
class person
{
public:
	char name[64];//string本身是一个类，尽量不要读取自定义的类型中有string，会吧类写进去
	//char是c语言的字符串
	int age;

};
void test()
{
	//1,包含头文件
	//2，创建流对象
	ifstream ifs;
	//3,打开文件，判断文件是否打开成功
	ifs.open("person.tex", ios::in | ios::binary);
	if (!ifs.is_open())
	{
		cout << "打开文件失败" << endl;
		return;
	}

	//4,读 文件
	person p = { "ahelly",20 };
	ifs.read(( char*)&p, sizeof(person));//强转
	cout << p.name << endl << p.age << endl;

	//5,关闭文件
	ifs.close();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



### 总结

![](https://s3.bmp.ovh/imgs/2021/12/711b8b1a5e6412d3.png)

流对象的创建都是 `ofstream ofs;`

打开文件，二进制需要强调`ios::binary`

写文件，二进制使用 write()函数，文本直接`ofs`<<



![](https://s3.bmp.ovh/imgs/2021/12/7c619ac46fc4e28d.png)

- 流对象创建都是` ifstream ifs;`

- 打开文件的同时都要判断是否打开成功

打开文件：`ifs.open("路径"，打开方式)`

判断:`if(!ifs.is_open())`

- 读文件

文本文件有四种方式读文件 

二进制文件使用到 read() 函数

