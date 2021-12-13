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



