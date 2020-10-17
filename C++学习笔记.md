<center><font size=6 color='blue'>C++学习笔记</font></center>

<center>based on the book 《A Complete Guide to Programming in C++》</A></center>

[toc]

---

# Chapter  1 Fundamentals 主体结构

* First C++ program

  ```C++
  #include <iostream>		//preprocessor
  using namespace std;	//standard
  int main()				//only one
  {
  	cout << "Hello world!" << endl;
  	return 0;			//terminate a program correctly
  }	
  ```

  screen out:Hello world!

* comment 注释

  ```C++
  //单行注释，//后的被注释掉
  /*多行
  注释*/	//    /*content*/:content被注释掉
  ```

---

# Chapter  2 Fundamental Types, Constants, and Variables 基本类、常量、变量

## 2.1 基本类 fundamental types

* bool type

  `true` or `false`，`0`也是`false`，其它数值为`true`。

* integral type

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200820222513058.png" alt="image-20200820222513058" style="zoom:67%;" />

​	signed:带符号的整数	unsigned：不带符号的整数，min=0
​	根据ASCII码，char与int（0-255）一一对应

* floating-point type

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200820223054483.png" alt="image-20200820223054483" style="zoom:67%;" />

​	float:单精度 double:双精度 long double:更高精度

* sizeof operator

  ```C++
  sizeof(double);	//8 bytes
  sizeof(a);		//float a; 4 bytes
  ```

* void type

  don't represent any value.

## 2.2 常量 constants

* boolean constants

  `true` or `false`:two states

* numerical constants

  decimal:十进制 octal: 八进制 hexadecimal：十六进制
1000UL：unsigned long integer 1000
  99.9F: floating-point number 99.9

* character constants

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200820225033974.png" alt="image-20200820225033974" style="zoom:67%;" />

​	'character constants':单引号

* string constants

  ```C++
  "I love you!"	//双引号，最后包含停止符'\0'
  "I love \
  you!"	// 单反斜杠\用于string内换行
  ```

* escape sequences 转义字符

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200820225532493.png" alt="image-20200820225532493" style="zoom:67%;" />

* name constants

  keywords in C++不能作为变量，对象等的名字

  * name:字母，数字，下划线组成
  * 首字母或首下划线

## 2.3 变量 variables

* defining and initializing variables

  ```C++
  char c;
  int i, counter(2);	//counter(2); 等于 counter=2;
  double x, y, size=9.9;
  ```

* constant objects

  ```C++
  const double x=9.9;	//const即read-only
  ```

---

# Chapter  3 Using Functions and Classes 函数和类

## 3.1 函数 function 

* prototype

  ```C++
  int pow(double, double);	//int:return type,double:argument type
  void pow(double x, double y);	//return type可为void，即无返回值
  int pow(void)	//without arguments
  ```

* definition

  ```C++
  int pow(double x, double y)
  {
      function block;
  }
  ```

* mathematical standard function

  ```C++
  #include <cmath>	//library for mathematical standard function
  a=sqrt(2);	//sin(),cos(),sqrt(),pow(),exp(),log(),log10()
  ```

* srand() and rand()

  ```C++
  //利用时间作为种子，生成随机数，涉及两个库ctime和cstdlib
  #include <ctime>	//time()
  #include <cstdlib>	//srand() and rand()
  long long sec;
  time( &sec); // Get the time in seconds.
  srand((unsigned)sec); // Seeds the random number generator
  randnum = rand();
  ```

## 3.2 类 Class

* standard class(header files)

  ```C++
  #include <iostream>		//<cstdlib>和"stdlib.h"一致的
  using namespace std;
  ```

* using class

  ```C++
  #include <string>	//preprocess class string
  string s("I am a string");
s.length();			//object.method();
  getline(cin, s);	//global functions in class string
  ```

---

# Chapter  4 Input and Output with Streams 输入输出流

* streams

  `cin`:standard input			`cout`:standard output
  `cerr`:unbuffered error output  `clog`:buffered error output

​	I/O stream class:`#include <iostream>`
​    istream:`>>`	ostream:`<<`

* formatting and manipulators

  ```C++
  cout << showpos << 123; // Output: +123
  cout.setf( ios::showpos); cout << 123;	//equivalent to above statement
  cout << 22; // Output: +22
  cout << noshowpos << 123; // Output: 123 unsigned
  cout.unsetf( ios::showpos);  cout << 123;
  ```

* input methods

  ```C++
  int x;	string s;
  cin >> x;	//input x from keyboard,if x isn't a integer, cin>>x is false.
  cin.get(x);	//从缓冲区输入x,不满足int type,返回false
  getline(cin, s, '.');//输入一行,teminate with '.'
  cin >> oct >> n;	//input an octal integer
  ```

* output formatting

  ```C++
  cout << hex << uppercase << 11; //Output: B	hex/oct/dec:16/8/10进制
  cout << dec << showpos << 11; //Output: +11
  cout.precision(2);	//设置输出精度 or:cout << setprecision(2);
  cout << scientific << 111 << endl;//科学计数，fixed:固定，showpoint:显示dot
  cout << setw(6) << left << 1;//Output:     1,field width 6 or:cout.width(6);
  						//left/right/internal对齐,default:right
  cout << setfill('*') << setw(5) << 12;// Output: ***12 or:cout.fill('0');
  cout << 'A';	//Output:A      character code:cout << int('0');
  //outputting string和输出数值方法一致，manipulators均可用
  bool ok = true;    cout << ok << endl // 1
  		<< boolalpha << ok << endl; // true     manipulator:boolalpha/noboolalpha
  ```

---

# Chapter  5 Operators for Fundamental Types 基本计算

* binary arithmetic operators

  `+,-,*,/,%取整`

* unary arithmetic operators

  `(+ -)正负号,++ increment,--decrement`
  ``++i`的值为i=i+1后的i值,`i++`的值为i=i+1后的i值,`--i,i--`同理

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200821110841629.png" alt="image-20200821110841629" style="zoom:67%;" />

* assignments

  `i+=1`:`i=i+1`,`-=,*=,/=,%=`同理
  `i+=1+2`:`i=i+(1+2)`

* relational operators

  `<,<=,>,>=,==,!=`返回值为bool:true or false

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200821112052040.png" alt="image-20200821112052040" style="zoom:67%;" />

* logical operators

  `&&(and),||(or),!(not)`返回值为bool:true or false，
  eg:(bool)||(nool),!(bool)  cin>>x返回值为bool,可用于逻辑判断

---

# Chapter  6 Control Flow 控制流

## 6.1 循环体 loop

* while

  ```C++
  while( expression ) //syntax	expression:bool type,cin>>x可以的
  	{statement;}		 // loop body，单行代码可不用{}，也可只有;
  ```

* for

  ```C++
  for( expression1; expression2; expression3 )//依次，expression2判断for是否继续
      								//expression1~3均可为多个代码，用','隔开
  	{statement;}	// loop body，单行代码可不用{}，也可只有;
  ```

* do-while

  ```C++
  do					//先运行一次statement，再判断
  	statement
  while( expression);	//attention:最后有一个';'
  ```

## 6.2 选择体 selection

* if-else

  ```C++
  if( expression )	//判断expression,执行statement1 or statement2
  	{statement1;}
  else
  	{statement2;} 	//else可有可无
  ```

* else-if chains

  ```C++
  if ( expression1 )		//从上到下执行多次判断，直到true
  	statement1
  else if( expression2 )	//cin>>x or cin.get(s)返回值为bool,可以作为expression
  	statement2
  ...
  else if( expression(n) )
  	statement(n)
  [ else statement(n+1)]
  ```

* switch

  ```C++
  switch( expression )	//判断expression与各const是否一致
  {						//switch可由else-if chains实现
  	case const1: [ statement ]
  				[ break; ]
  	case const2: [ statement ]
  				[ break; ]
  	...
  	[default: statement ]
  }
  ```

* conditional operator

  ```C++
  expression ? expression1 : expression2; //判断expression,true返回ex1,false返回ex2
  ```

## 6.3 跳跃 jump

* break

  `break;`跳出loop

* continue

  `continue;`不执行后续的loop body,进入下一个循环

* goto

  ```C++
  for( . . . )
  	for( . . . )
  		if (error) goto errorcheck;//error is true,执行errorcheck
  	. . .
  errorcheck: . . . // Error handling
  ```

---

# Chapter  7 Symbolic Constants and Macros 符号常量和宏

* definition

  ```C++
  #define name substitutext	//defining syntax
  #define PI 3.1415926		//symbolic constant
  #define SQUARE(a) ((a) * (a)) //marco with parameters
  ```

* redifining marcos

  ```C++
  #define MIN(a,b) ((a)<(b)? (a) : (b)) //重新定义（之前已定义过MIN）
  	. . . // Here MIN can be called
  #undef MIN
  ```

* conditional inclusion

  ```C++
  #ifndef _BASIS_H_	//标识头文件"basis.h"
  #define _BASIS_H_	//其它.h或.cpp，可通过#include "basis.h"使用
  ...
  #endif
  ```

* standard marcos for character

  `isalpha(c)`字母？ `islower(c)`小写字母？ `isupper(c)`大写字母？ `isdigit(c)`数字？`isalnum(c)`字母或数字？`isspace(c)`空格符？`isprint(c)`可打印字符？

  `toupper`,`tolower`转换为大写，小写

  上述marcos的使用，均需要`#include <cctype>`or`#include <ctype.h>`，is返回bool,to返回对应转换的字符（段）

* filter programs

  ```C++
  while(cin.get(c)) {...}
  while(getline(cin,line)) {...}
  ```

---

# Chapter  8 Converting Arithmetic Types 算术类型转换

1. 隐式类型转换

编译器自动执行隐式类型转换，其中为两个操作数的值分配一个允许执行相关操作的通用类型。通常可以假设“较小”类型将转换为“较大”类型。

* `bool`，`char`，`signed char`，`unsigned char`和`short`都将转换为`int`.

* 如果`int`类型大于`short`，则`unsigned short`也将转换为`int`，而在所有其他情况下，也将转换为`unsigned int`。

* `int->double->float`

* 当函数输入的type与prototype不一致时，可以自动执行隐式类型转换，eg:

  ```C++
  void func( short, double); // Prototype
  int size = 1000;
  // . . .
  func( size, 77); // Call 隐式转换：1000(int)->1000(short),77(int)->77.0(double)
  ```

2. 显示类型转换

​	`(type) expression`将expression的类型转换为type类型，`(type)`运算符的优先级高于算术运算符。

---

# Chapter  9 The Standard Class string 字符串类

* initializing

  ```C++
  #include <string>	//preprocess the class string
  string message("Good morning!");	//initializing a string
  		line(50, '-');
  cout << message.length(); // Output: 13 string类的method:length(),size()
  ```

  string的储存不包括`'\0'`

* input string

  ```C++
  cin >> s;	//input a word
  getline(cin, s, '.');	//input a line of words, terminate with a '.'
  ```

* concatenate strings

  ```C++
  string sum, s1("sun"), s2("flower");
  sum = s2 + s3;	//+
  sum += s2;	//+=
  ```

* compare strings

  ```C++
  string s1("AA"), s2("aa");
  s1 == s2;	//s1<s2;从第一个字符进行比较，完全相同，有s1=s2，'A'<'a',所以s1<s2
  ```

* methods of class string

  ```C++
  s.length();				//返回string长度or:s.size()
  s.insert(5, "aaaa", 1, 2);	//在s的第5位置插入"aaaa"的从第1位置的前2个字符
  s.erase(4,7); 			// 清除，Start position: 4, Quantity: 7
  s.replace(6, 4, s1, 1, 3);	//用s1的从第1位置的3个字符替换s的从第6位置的4个字符
  int first = youth.find("young");	//返回search位置，左起
  int last = youth.rfind("young");	//返回search位置，右起
  s.at(i) = 'X'; 				//is equivalent to s[i] = 'X';
  ```

* access character in string

  `standard marcos for character:isspace()之类的`

* subscript operator

  string可视为数组，可对某个字符进行替换，也是从0开始

  ```C++
  s.at(i) = 'X'; 				//is equivalent to s[i] = 'X';
  ```

---

# Chapter 10 Function 函数

* Libraries

  C ++标准库提供了许多有用的全局函数和类。此外，您可以将其他库用于特殊目的。通常，编译器软件包将提供商业类库或图形用户界面。
  通常将属于在一起的类和函数复合在一起以形成单独的源文件，这些文件可以独立地编译和测试。

* Defining function

  ```C++
  void test( int, double ); 				// Prototype   //can omit parameter names arg1
  int main()
  {...
  	test( 10, -7.5); 						// Call
  ...}
  void test(int arg1, double arg2 ) {...}	// Definition      
  //sytnx:[type] name([declaration_list]) 	[type]:return type and void means no return
  ```

* Passing arguments

  ```C++
  test( 10, -7.5);	//pass by value;arg1=10,arg2=-7.5;原始值不变
  int x=10;
  double y=-7.5;
  test(x,y);	//pass by reference if definition is void test(int& arg1, double& arg2);x,y可能变
  ```

  another method:[pass by reference](##12.1 reference) ,[pass by pointer](12.2 pointer)

* Local objects
  * func1()函数和func2()函数中包含变量a。变量不会冲突，因为它们引用了不同的内存地址。
  * 函数的本地对象放置在==堆栈==(stack)上。堆栈是根据LIFO（后进先出）原则进行管理的内存区域。LIFO原则可确保首先销毁创建的最后一个本地对象。

* inline function

  编译器将==内联函数==的代码插入调用该函数的地址，从而避免跳转到子例程。

  ```C++
  inline int max( int x, int y)
  { return (x >= y ? x : y ); }
  ```

* Defining default arguments

  ```C++
  void moveTo( int x = 0, int y = 0);	//void moveTo( int = 0, int = 0);
  moveTo (); moveTo (24); moveTo(24, 50);		//ok
  ```

* Overloading

  不同函数能可以具有相同的名称。==重载==

  ```C++
  int max( int x, int y);
  double max( double x, double y);
  ```

* Recursion

  调用自身的函数被称为==递归==的。始终需要一个中断条件来避免让函数无限地调用自身。

---

# Chapter 11 Storage Classes and Namespaces 储存类和名字空间

## 11.1 storage classes

四种储存类：`extern`，`static`，`auto`，`register`。一个对象的定义包括：`type`，`name`，`storage class`。

`storage class`：一个对象从创建到销毁的周期（`lifetime`）。

* extern

  `extern`：external，外部，即创建全局变量（global object），外部对象使得可以在任何函数之间交换信息而无需传递任何参数。

  ```C++
  extern long position;	//extern type name;
  ```

  extern声明仅引用一个对象，不应用于初始化该对象。 如果确实初始化了该对象，相当于正在定义该对象！

* static

  `static`：整个程序周期，program结束时，对象销毁。不是储存在堆栈上的。有两种情况：

  1.external：外部静态，也就是说，只能在模块内使用其名称来指定该对象，而不会与其他模块中使用相同名称的任何对象发生冲突。

  2.within block：内部静态，也就是说，该对象仅在单个块中可见。 但是，该对象仅创建一次，并且在离开该块时不会被破坏。 重新进入块时，您可以继续使用原始对象。

  ```C++
  static int count;		//static type name;
  ```

* auto

  `auto`：automatic，代码块内，局部变量，离开block时，对象销毁。当程序流到达定义时，将在堆栈上创建对象，但是与静态类型的对象不同，该对象在离开块时被破坏。

  ```C++
  auto float radius;		//equivalent to float radius;
  ```

* register

  `register`：为了提高程序速度，可以将常用的自动变量存储在CPU寄存器中，而不是存储在堆栈中。变量不能太大，常用type：`char`，`short`，`int`，`pointer`。

  ```C++
  register int x;			//register type name;
  ```

* storage class for function

  ```C++
  extern bool getPassword(void);		//external function
  static long timediff( void );		//static function
  ```

## 11.2 namespace

C ++提供了名称空间的使用，以避免与全局标识符的命名冲突。 在名称空间内，您可以使用标识符，而无需检查它们是否先前已在名称空间之外的区域中定义。 

* defining namespace

  ```C++
  namespace myLib
  {
  	int count;
  	double calculate(double, int);
  	std::string mess="love";	//without:using namespace std;
  }
  myLib::count = 7;		//outside of myLib
  ```

  使用范围解析运算符::来引用全局名称，即在任何名称空间之外声明的名称。 为此，只需省略名称空间的名称。`::demo();`

  * 不需要连续定义名称空间。 您可以在程序中的任何位置重新打开和扩展先前定义的名称空间。

  * 可以嵌套名称空间，即可以在另一个名称空间中定义一个名称空间。

* keyword using

  可以使用using声明或using指令简化对命名空间元素的访问。 在这种情况下，您无需重复引用名称空间。 就像普通的声明一样，使用声明和using指令可以出现在程序的任何部分。

  ```C++
  using namespace std;	//no need of std::cout	using directive
  using std::cout:        //seperately use cout	using declararion
  ```

---

# Chapter 12 References and Pointers 引用与指针

## 12.1 reference

* define reference

  ```C++
  float x = 17.232F;
  float& rx = x;		//or:float &rx = x; a reference to x;
  &rx			//address of rx, thus is equal to &x.
  int a; const int& cref = a; const double& pi = 3.1415926 // ok! read-only reference
  ```

  引用的定义不占用额外的储存空间。引用必须在声明时初始化，并且以后不能修改。

* pass by reference

  引用类型的参数是参数的别名。 调用函数时，将使用提供的对象作为参数初始化参考参数。 因此，该函数可以直接操纵传递给它的参数。

  ```C++
  void test( int& a) { ++a; }
  test( var); 
  void display( const string& str);	//define a read-only reference as parameter.
  ```

  如果通过引用传递对象时将其作为参数传递，则不会复制该对象。 相反，对象的地址在内部传递给函数，从而允许函数访问调用它的对象。

* reference as return value

  ```C++
  double& refMin( double&, double&);
  const string& message();	//read-only
  ```

## 12.2 pointer

指针是一个表示另一个对象的地址和类型的表达式。使用地址运算符＆为给定对象创建指向该对象的指针。

* define pointer

  ```C++
  int a, *p, &ra = a;	//define variable, pointer, reference, default: NULL pointer
  p = &a;		//let p point to a
  *p = 12.3;	//equal to a = 12.3
  *p += 2;	//equal to a = a + 2
  double y = sin(*p);		//equal to y = sin(a)
  ```

* pass by pointer

  ```C++
  long func( int *iPtr ) {/* Function block */}
  long y = func( &x )
  ```

---

# Chapter 13 Defining Classes 定义类

* define class

  `private`：私有成员，不能从外部访问。成员访问的默认值为私有。

  `public`：公共成员，可以从外部访问。

  ```C++
  class Demo					//Class names begin with an uppercase letter
  {
      private:				//member names begin with a lowercase letter.
      //... Private data members and methods here
      public:
      //... Public data members and methods here
      type init() {...}		//methods
  }
  type class_name::function_name(parameter_list) { . . . }
  
  Demo A, B;	//define objects
  ```

* define, access and call

  ```C++
  // account.h
  // Defining the class Account.
  // ---------------------------------------------------
  #ifndef _ACCOUNT_ 				// Avoid multiple inclusions.
  #define _ACCOUNT_
  #include <iostream>
  #include <string>
  using namespace std;
  class Account
  {
  private: 					// Sheltered members:
  	string name; 			// Account holder
  	unsigned long nr; 			// Account number
  	double balance; 			// Account balance
  public: 					//Public interface:
  	bool init( const string&, unsigned long, double);
  	void display();
  };
  #endif // _ACCOUNT_
  
  // account.cpp
  // Defines methods init() and display().
  // ---------------------------------------------------
  #include "account.h" // Class definition
  #include <iostream>
  #include <iomanip>
  using namespace std;
  bool Account::init(const string& i_name,unsigned long i_nr,double i_balance)
  {/*...*/}
  void Account::display() {/*.../*}
  
  // account_t.cpp
  // Uses objects of class Account.
  // ---------------------------------------------------
  #include "account.h"
  int main()
  {
  	Account current1, current2, *ptr = &current1;		//define objects
  	current1.init("Cheers, Mary", 1234567, -1200.99); //call methods
  	current1.display();
  	//access:object.member     object.method()
  	//assign:current1 = current2;
  	//pointer to object:ptr->method();      equal to *ptr.method();
  	return 0;
  }
  ```

* struct

  ```C++
  struct Date { short month, day, year; };
  //just like: class Date { public: short month, day, year;};
  Date birthday(1, 2, 1998);
  ```

* union

  联合（`union`）不能同时将多个数据成员存储在同一地址。

  ```C++
  union Number			//default setting: public
  {
  	long n;
  	double x;
  };
  Number number1, number2;
  ```

---

# Chapter 14 Methods 类方法

* constructor

  定义对象后，C ++会执行隐式初始化。这样可以确保对象始终具有有效的数据进行处理。初始化是通过称为==构造函数==的特殊方法执行的。构造函数名字即类名字，无返回值，即`void`。构造函数根据参数可重构。

  ```C++
  class Account
  {
  private: 
  public: 
  	Account( const string&, unsigned long, double );		//constructor
  	Account( const string& );
      ~Account();			//destructor
  };
  Account::Account( const string& a_name, unsigned long a_nr, double a_state) {/*...*/}
  Account::Account( const string& a_name ) {/*...*/}
  Account::~Account() {/*...*/}	
  Account giro("Cheers, Mary", 1234567, -1200.99 ), save("Lucky, Luke");   //call constructor
  ```

  如果一个类不包含构造函数定义，则编译器将创建最小版本的默认构造函数作为公共成员。

* destructor

  对象的各个数据成员总是按照与创建它们相反的顺序删除。 因此，将首先清理要创建的第一个数据成员。 如果数据成员也是类类型的对象，则将调用该对象自己的==析构函数==。用法如上code block。

  在对象生命周期结束时会自动调用析构函数：

  * 对于局部对象（属于静态存储类的对象除外），在定义对象的代码块末尾。
  * 对于全局或静态对象，在程序末尾。

* inline method

  持续调用“短”`method`会影响程序的运行时间。实际上，与执行函数本身相比，保存重新输入地址并跳转到被调用函数再返回到调用函数可能会花费更多时间。为了避免这种开销，可以以类似于定义==内联全局函数==的方式来定义内联方法。

* access method

  ==访问方法==提供了一种访问私有数据成员的更为有用的方法。访问方法允许以受控方式读取和操作数据。如果将访问方法定义为内联，则访问与对公共成员的直接访问一样有效。`set(),get()`。

* const

  ```C++
  const Account inv("Lucky, Luke");	//must be initialized  const object
  long getName() const {/*...*/}		//read-only method
  ```

  每个类自动包含四个标准方法：默认构造函数、析构函数、复制构造函数和赋值。

* this pointer

  可通过常量指针`this`用于指向当前对象的地址。

  ```C++
  Class_id* const this = &actObj;
  this->data;  //equal to actObj.data
  ```

* pass object as argument

  ```C++
  bool isLess( DayTime t) const;
  bool isLess( const DayTime& t) const;
  bool isLess( DayTime* t) const;
  ```

  返回值可以为`object`，`reference`，`pointer`。

---

# Chapter 15 Member Objects and Static Members 成员对象和静态成员

属于一个类别的数据成员可以是另一个类别的对象。因此，Account类的对象具有字符串类型的成员子对象，或简称为成员对象。如果一个类包含类型不同的数据成员，则这些类之间的关系称为==“Has-A”==关系。

* member initializer

  ```C++
  Result::Result( /* Parameters */ )			//just like a constructor
  : val(w), time(hr, min, sec)
  { /* Function block */ }
  ```

* static member

  每个对象都有自己的特征。 这意味着两个不同对象的数据成员将存储在不同的存储器地址中。但是，有时保留一些可以被一个类的所有对象访问的公共数据很有用，例如：

  * 诸如汇率，利率或时间限制之类的数字，每个对象具有相同的值。
  * 状态信息 ，例如对象的数量，当前的最小或最大阈值或指向某些对象的指针； 例如，指向窗口类中活动窗口的指针。

  ```C++
  static double rate;		//all objects are same
  static double Min, Max;  //all objects have only one data
  static double getMin();  //static method
  ```

  由于静态数据成员独立于任何对象，因此对其的访问也应独立于任何对象。静态成员函数用于此目的。例如，即使该类中不存在任何对象，也可以为该类调用静态成员函数。

* enumeration

  ==枚举==是用户可定义的整数类型。使用enum关键字定义枚举。值的范围和这些值的名称也同时定义。

  ```C++
  enum Shape{ Line, Rectangle, Ellipse}; //{0, 1, 2}
  enum Shape{ Line, Rectangle=0, Ellipse}; //{0, 0, 1}
  enum Shape{ Line=-100, Rectangle=0, Ellipse=100}; //{-100, 0, 100}
  ```

---

# Chapter 16 Arrays 数组

## 16.1 一维数组 array

* Defining arrays

  ```C++
  float arr[10]	//type name[count]
  ```

* Initializing arrays

  ```C++
  int arr[3] = {1, 2, 3}	//[]中3也可以不要
  int arr1[4] = {1, 2, 3}	//arr1={1, 2, 3, 0}
  int arr2[2] = {1, 2, 3}	//arr2={1, 2}
  ```

* Char arrays

  ```C++
  # include <cstring>			//char-related library
  char text[40] = "Hello Eve";	//text最后一位为'\0'停止符
  ```

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200820184618320.png" alt="image-20200820184618320" style="zoom:67%;" />

* Class arrays

  ```c++
  Account accountTab[] =		//Class_type name[]={...Account object...};
  {
  	Account("Tang, Sarah", 123000, 2500.0),
  	Account("Smith, John", 543001),
  	Account(), 			// Default constructor
  	"Li, Zhang", 		// Account("Li, Zhang"),
  	giro 				// Account(giro) giro-existed Account object
  };
  accountTab[0].setState(1000.0); //method可用 
  							//=Account("Tang, Sarah",123000, 1000.0),
  ```

## 16.2 多维数组 matrix

* Defining and initializing

  ```C++
  char representative[2][20] = {"Armstrong, Wendy",	//[m][n]:m行n列,from 0
  							"Beauty, Eve"};
  int articleCount[2][5] = { { 20, 51, 30, 17, 44},	//articleCount[0][0]=20;
  						{150, 120, 90, 110, 88}};	//articleCount[9]=88;
  ```

* Bubble sort algorithm

  冒泡排序算法：该算法反复访问数组，比较相邻的数组元素，并在需要时交换它们。当没有更多元素需要交换时，排序算法终止。

---

# Chapter 17 Arrays and Pointers 数组和指针

* name pointer

  数组名称是指向第一个数组元素的指针。

  ```C++
  char ptr = "Hello!";
  cout << ptr;	//is equivalent to cout << &ptr[0];   result:p
  cout << (void*)ptr;	//display the address in hexadecimal format
  ```

  指针和数组间存在相应关系：

> arr[i] is equivalent to *(arr+i)	//arr+i is a pointer point to arr[i]
>
> &arr[i] is equivalent to (void*)(arr+i)

* pointer arithmetic

  ```C++
  *ptr++;	// *(ptr++) :*(ptr+1). *,++,--have same precedence. move a point.
  int index = pv - v;	//pv points to v[3],pv-v=3 is assigned to index. point subtracting
  pv >= v;	//compare two pointers:pv>=v is true;
  ```

* strcpy

  The standard function strcpy() copies C strings

  ```C++
  char dest[30], source[] = "A string";
  strcpy( dest, source);	//copy source to dest
  void strcpy( char *s1, char *s2) // Copy s2 to s1.
  {
  	while( (*s1++ = *s2++) != '\0' ) // Copy and append
          ; 							// terminating character
  }
  ```

  通常，指针版本比索引版本更好，因为它们更快。

* Pointers to const Objects

  如果需要指向常量对象，则必须使用只读指针。

  ```C++
  const int a, b, *p=&a;
  cout << *p;	//read is okay
  *p = 1;	//error! Because *p is a const object which cannot be modified.
  p = &b;	//ok!
  int strlen( const char *s);	//Read-only pointer as parameters
  ```

  只读指针也可以指向非常量对象。如果可以将常量对象作为参数传递，则需要声明一个只读指针。

* strcpy() & strcat() & strstr() & strncmp()

  标准函数`strcpy()`==复制==C字符串，并将作为第二个参数传递的C字符串复制到第一个参数中。

  标准函数`strcat()`==连接==两个C字符串，并将作为第二个参数传递的C字符串添加到第一个参数中。

  标准函数`strstr()`在字符串中==搜索==给定的字符序列。 

  标准函数`strncmp()`用于==比较==两个字符串。

* pointer array

  ```C++
  Account save("A", 1000.00),
  		depo("B", 2000.00);
  Account *accPtr[5] = { &depo, &save, NULL};	//initialization,NULL value for pointer(not use)
  ```

---

# Chapter 18 Fundamentals of File Input and Output 文件输入和输出

## 18.1 Open file

高效便捷的文件管理意味着将需要存储的数据放入所谓的文件缓冲区`(buffer)`的主存储器中的临时存储中。

* file stream

  ```C++
  #include <fstream>
  ifstream myfile("test.fle");	//filename:test.fle  	file stream name:myfile
  ofstream yourfile("new.fle");	//it must be careful.It may destroy existed file with same 
  //ofstream yourfile;														name	
  //yourfile.open("new.fle");
  ```

  <img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200907090959379.png" alt="image-20200907090959379" style="zoom:67%;" />flags for open mode of a file

* open mode

  如果引发`ios :: in`标志，则该文件必须已经存在。 如果未使用标志`ios :: in`，则创建该文件（如果尚不存在）。`open() method`也是如此，`yourfile.open("new.file", ios::out | ios::app);`。

  ```C++
  fstream addresses("Address.fle", ios::out | ios::app);
  //This opens a file for writing at end-of-file.
  fstream addresses("Address.fle", ios::in | ios::out);
  //to open an existing file for reading and writing.   default mode.
  ```

* error handing

  ```C++
  if(!myfile)	//or:if(myfile.fail())
  if(myfile.eof())	//end of file?
  ```

## 18.2 close file

* open() & is_open()

  ```C++
  myfile.close();	//close file but stream is still existing
  if(myfile.is_open())	//open or not
  {/*...*/}
  void exit( int status );	//terminate a program
  ```

## 18.3 read and write

* input and output

  ```C++
  //get(),getline(),put(); for read
  double price = 12.34;
  ofstream textFile("Test.txt");	//existing file
  textFile << "Price: " << price << "Dollar" << endl;//write into file like screen output
  ```

* transferring data blocks

  ```C++
  if(!filestream.write("An example", 2))			//write() method
      cerr << "Error in writing!" << endl;
  istream& read(char *buf, int n);			//read() method
  ```


---

# Chapter 19 Overloading Operators 重载运算符

运算符重载==规则==：不能创建“新运算符”，即，只能重载现有运算符。不能为基本类型重新定义运算符。不能更改运算符的操作数。 二元运算符将始终为二进制，一元运算符将始终为一元。具有相同优先级的优先级和分组运算符的顺序保持不变。

* operator function

  两种重载运算符的方式：1.定义为类中的`method` 2.定义为全局函数`global operator function`。

  ```C++
  class DayTime
  {
      private://...
      public://...						//overload operator < and ++
      bool operator<(const DayTime& t) const {/*...*/}	//binary operator
      DayTime& operator++() {/*..*/}						//unary operator
  };
  inline DayTime operater+(const DayTime& t1, const DayTime& t2) {/*...*/} //global function
  if(day1<day2) {/*...*/}		//call overload operator  is equal to day.operator<(day2) 
  y = x + 10; //ok, but y = 10 + x is not okay if operator is overloaded as a method. But it 				// is okay for global operator function.
  ```

  运算符函数被定义为方法，尤其是在一元运算符的情况下。

  可以将全局运算符函数声明为该类的“朋友”`friend`，以允许其访问该类的私有成员。

  ```C++
  class Euro
  {
      private://...
      public:
      //...
      friend Euro operator+( const Euro&, const Euro&);
  };
  inline Euro operator+( const Euro& e1, const Euro& e2)
  {
      Euro temp;
      temp.data = e1.data + e2.data;
      return temp;
  }
  ```

* friend class

  除了函数可申明为`friend`，类也可以申明为`friend`。如果一个类与另一个类紧密结合使用，以致该类中的所有方法都需要访问另一个类的私有成员，定义为`friend class`很有用。`friend class`最好定义在`public`。

  ```C++
  class A
  {
    private://...
    public:
      friend class B;
  };
  ```

  定义为`friend`需谨慎，这会破坏数据封装。

* subscript operator

  限制适用于非重载的索引运算符：1. 一个操作数必须是一个指针，例如一个数组名。2. 其他操作数必须是一个整数表达式。

---

# Chapter 20 Type Conversion for Classes 类的类型转换

隐式和显式类型转换也针对C++中的类执行。可以决定允许哪种转换。可以允许不同类之间或类与基本类型之间进行类型转换。有两种转换：

* conversion constructor

  ```C++
  Euro::Euro( int ); 		// int -> Euro			conversion constructor：
  Euro::Euro( double ); 	// double -> Euro			standard type to other type
  Euro my(100), 			// int-> Euro,
  your(321.41); 			// double -> Euro.
  my = 987.12; 			// Implicit conversion: double -> Euro
  your += 20; 			// Implicit conversion: int -> Euro
  your = Euro(999.99); 		// Explicit conversion (constructor style)
  my = (Euro)123.45; 			// Explicit conversion (cast style)
  your = my; 					// No conversion
  ```

* conversion function

  定义了如何执行转换。 编译器还自动使用转换函数来执行隐式和显式类型转换。

  ```C++
  class Euro
  {//as before
      public:
      	operator double() {return (double)data/100.0;}     //define conversion function
  };
  Euro salary(8888.88);
  double x(0.0);
  salary += 1000;	// implicit int -> Euro
  salary += 0.10;	// implicit double -> Euro
  x = salary;
  x = (double)salary;				// explicit Euro -> double by standard conversion
  x = salary.operator double();	 // explicit Euro -> double by using conversion function
  x = double(salary);				// explicit Euro -> double by using conversion function
  int i = salary;					// explicit Euro -> int by standard conversion
  ```

* explicit conversion

  ```C++
  explicit Euro( int euro = 0, int cents = 0);
  double asDouble() const { return (double)data/100.0;}
  salary = Euro( 7777.77); 		// explicit double -> Euro
  salary += Euro(1000.10);
  x = salary.asDouble(); 		// explicit by method Euro -> double
  int i = salary.asDouble(); // Euro -> double -> int
  ```

  

---

# Chapter 21 Dynamic Memory Allocation 动态内存分配

* new and delete

  C++使用`new`和`delete`运算符分配和释放内存，这意味着可以创建和销毁任何类型的对象。

  ```C++
  double *ptr;
  ptr = new double(99.99);	//ptr is a pointer to double with a value 99.99 /allocate memory
  delete ptr;	//destroy memory
  Euro* europtr = new Euro( -123.45);		//explicit initialization
  cout << europtr->getCents() << endl;	//*europtr.getCents()
  ```

  可以使用`delete`运算符释放通过调用`new`分配的内存。对于未用`new`分配的内存是不能用`delete`清除的。

  * 不要对同一对象两次调用`delete`。
  * 不要使用`delete`释放静态分配的内存。

* new[] and delete[]

  `new[]`运算符可用于创建动态数组。调用运算符时，必须提供数组元素的类型和数量。`delete[]`运算符可用于销毁动态数组。

  ```C++
  Account* pArr = new Account[256];	//pArr[i] is equal to *(pArr+i).
  delete [] pArr;		//destroy pArr memory;
  ```

* linked list

  链表（`linked list`）是一种动态数据结构，可轻松插入和删除数据。 数据结构定义了如何以单位，存储和操作数据的方式来组织数据，例如数组，列表或树。

  每个列表元素包含一个用于实时数据的数据存储，以及一个指向列表中下一个元素的指针。

  * 仅在需要时分配列表元素的内存。
  * 在插入或删除列表元素时，仅需要移动指针。

---

# Chapter 22 Dynamic Members 动态成员

可以利用动态内存分配的潜力来利用现有的类并创建可变长度的数据成员。根据应用程序真正需要处理的数据量，在应用程序运行时会根据需要分配内存。为此，该类需要一个指向动态分配的包含实际数据的内存的指针。

* dynamic member

  ```C++
  class FloatArr
  {
    private:
      float *arrPtr;
      //...
    public:
      FloatArr(int n = 256);
      ~FloatArr()
  };
  FloatArr::FloatArr(int n) {arrPtr = new float[Max];}	//pointer to dynamic memory
  FloatArr::~FloatArr() {delete[] arrPtr;}	// destructor
  ```

* overload operator

  ```C++
  FloatArr& FloatArr::operator=(const FloatArr& src)
  {
      if(this != &src)
      {
          Max = src.Max; cnt = src.cnt;
          delete[] arrPtr;				// release memory
          arrPtr = new float[Max];			// allocate memory
          for(int i=0; i<cnt; ++i)
              arrPtr[i] = src.arrPtr[i];
      }
      return *this;
  }
  ```

---

# Chapter 23 Inheritance 继承

==继承==允许在现有类的基础上构造新类。新的派生类“继承”了所谓的基类的数据和方法。但是您可以为新类添加更多特征和功能。

我们区分`is`关系和所谓的`has`关系。当一个类的成员具有另一种类型时，在两个类之间会发生`has`关系,`is`关系是指一个类成员属于另一个类成员，基类B的所有公共成员`public`在派生类C中都是公开可用的。。

继承包括数据提取`data abstraction`和重使用`reusability`。

* derived class

  ```C++
  class C : public B			// class C is a derived class from class B
  {
  private:
  // Declaration of additional private data members and member functions
  public:
  // Declaration of additional public data members and member functions
  };
  ```

  搜索方法名称时，应遵循以下规则：

  * 编译器首先查找在派生类中调用的方法的名称

  * 如果找不到该名称，则编译器将向前走一步，并寻找一个公共的方法。

* redefinition

  派生类C可以有基类相同名字的`method`，在派生类C中成员函数和数据成员都可以被重新定义`redifined`。如果在派生类中重新定义成员，则它将在基类中屏蔽相应的成员。

  重新定义不会重载函数，因为派生类具有不同的范围。

  必须将range运算符`::`与基类的名称一起使用。否则，派生类中的`display()`方法将自行调用并进行不确定的递归。

  ```C++
  void C::display() const
  {
      B::display();	// methods in base class
      // ...
  }
  bb.display();		// call the display() in the derived class
  cc.B::display();	// call the display() in the base class
  ```

* constructor calls

  ```C++
  // first version
  PassCar::PassCar(const string& tp, bool sr, int n, const string& hs)
  {
      setNr(n);           // initialization of base class
      setProd(hs);
  
      passCarType = tp;   // initialization of derived class
      sunRoof = sr;
  }
  // second version
  PassCar::PassCar(const string& tp, bool sr, int n, const string& hs):Car(n, hs)
  {
      passCarType = tp;   // initialization of derived class
      sunRoof = sr;    
  }
  // third version
  PassCar::PassCar(const string& tp, bool sr, int n, const string& hs)
      :Car(n, hs), passCarType(tp), sunRoof(sr)
  {
      // there remains nothing to do
  }
  ```

* protected members

  为了允许`method`和`friend function`访问基类的`protected`成员，在私有和公共之间引入更高级别的访问控制。这是通过`protected`的声明来实现的。这意味着，受保护的成员无法访问基类对象以及从基类派生的任何类。但是，与私有成员相反，派生类的方法和朋友功能可以访问该成员。

  ```C++
  class Safe
  {
      private:
          int topSecret;
      protected:
          int secret;
          void setTopSecret(int n) {topSecret = n;}
          int getTopSecret() const {return topSecret;}
          void setSecret(int n) {secret = n;}
          int getSecret() const {return secret;}
      public:
          int nosecret;
          Safe()
          {topSecret = 100; secret = 10; nosecret = 0;}
  };
  class Castle:public Safe		// derived class member can call the protected member
  {
      public:
          Castle()
          {
              // topSecret = 10;    // Error, because private
              setTopSecret(10);
              secret = 1;
              nosecret = 0;
          }
  };
  Castle treasure;			// external objects can't call the private and protected member
  treasure.topSecret = 1; 	// Error: private
  treasure.secret = 2; 		// Error: protected
  treasure.setTopSecret(5); 	// Error: protected
  treasure.noSecret = 10; 	// ok
  ```


---

# Chapter 24 Type Conversion in Class Hierarchies 类层次的类型转变

可以将派生类的对象分配给基类的对象，这将导致隐式类型转换为基类类型。因此，基类成为多种特殊情况的通用术语。假定PassCar和Truck类是从Car类派生的，则始终可以像Car类型的对象一样管理PassCar或Truck类型的对象。

* implicit conversion

  ```C++
  #include "car.h"
  bool compare( Car&, Car&);
  int main()
  {
  	Car auto, *carPtr;
      PassCar beetle("New Beetle", false, 3421, "VW"),
  			miata( "Miata", true, 2512, "Mazda");
      auto = beetle; //data members additionally defined in the derived class are not copied!
      // beetle = auto; // Error!
      carPtr = &miata;
      carPtr->display();	// ok! carPtr->setSunroof(false); //Error!
      Car& carRef = cabrio; // ok
  	carRef.display(); 	// Output base members
  	carRef.setSunRoof(true); // Error
  	PassCar auto1;
  	auto1 = carRef; 		// Error
  	bool res = compare( beetle, miata);	// ok! Implicit conversion to base class.  
  // ...								   //Car& a = beetle; Car& b = miata;
  }
  bool compare( Car& a, Car& b)
  { //... }
  ```

* explicit conversion

  在向下转换指针或引用之后，可以访问派生类的整个公共接口。

  ```C++
  Car* carPtr = &cabrio;
  ( (PassCar*) carPtr )->display();
  static_cast<PassCar*>(carPtr)->display();
  ```


---

# Chapter 25 Polymorphism 多态

多态的实现方式分为三块：重载、重写、重定义。

* ==重载==是在同一作用域内（不管是模块内还是类内，只要是在同一作用域内），具有相同函数名，不同的形参个数或者形参类型。
* ==重写==是在不同作用域内（一个在父类一个在子类），函数名、形参个数、形参类型、返回值类型都相同并且父类中带有`virtual`关键字（换言之子类中带不带`virtual`都没有关系）。
* ==重定义==是在不同作用域内的（一个在父类一个在子类），只要函数名相同，且不构成重写，均称之为重定义。

* virtual method

  使用`virtual`定义虚拟方法，不需要在派生类中重新定义虚拟方法。派生类可以直接从基类继承虚拟方法。

  ```C++
  class Car
  {//...
  	virtual void display() const;
  };
  ```

  创建虚拟方法的专有版本意味着重新定义该方法。派生类中的重定义必须与基类中的虚方法具有

  * 相同的签名（名字）
  * 相同的返回类型。

* virtual destructor

  首先调用派生类的析构函数，然后执行基类的析构函数。

  如果在派生类中动态创建多个对象，则会发生危险情况。越来越多的未引用内存块将使主内存混乱，而无法重新分配它们，这会严重影响程序的响应，甚至导致外部内存被交换。

  用作其他类的基类的类应始终定义一个虚拟析构函数。 即使基类本身不需要析构函数，它也至少应包含一个伪析构函数，即具有空函数体的析构函数。

  ```C++
  virtual ~Base() {;}
  ```

* binding

  静态绑定（`static binding`）：当调用非虚拟方法时，在编译时就知道函数的地址。该地址直接插入到机器代码中。这也称为静态或早期绑定。如果通过对象名称调用虚拟方法，则在编译时也会知道该方法的适当版本。这也是早期绑定的情况。

  动态绑定（`dynamic binding`）：如果通过指针或引用调用虚拟方法，则在编译时将不知道程序运行时将执行的功能。

* virtual method table

  动态绑定使虚拟函数调用分两步执行：1.读取引用对象中VMT的指针。2.在VMT中读取虚拟方法的地址。

---

# Chapter 26 Abstract Classes 抽象类

* pure virtual method

  ```C++
  class A
  {//...
      virtual void demo()=0;	// pure virtual class
  }
  class B:public A
  {//...
      void demo();
  }
  int main()
  {
      A *ptr, &ref;	// ok. A ptr; is error.
      ptr = new B(parameters);
      ptr->income();
  }
  ```

  这将通知编译器该类中没有`demo()`方法的定义。然后，在纯虚拟方法的虚拟方法表中输入`NULL`指针。在派生类中定义该方法。

  不允许您创建任何对象的类称为==抽象类==。具有纯虚方法的类是抽象类。抽象类可以从具体类派生。尽管无法为抽象类定义对象，但是可以声明指向抽象类的指针和引用。

  * 必须为每个派生类定义用于赋值的虚拟操作符函数。

  * 为确保标准赋值也可用，还必须在每个派生类中重新定义标准赋值。

---

# Chapter 27 Multiple Inheritance 多重继承

一个类不仅可以包含一个，而且可以包含几个不同的基类。 在这种情况下，该类是在称为==多重继承==的过程中从多个基类派生的。

* multiply-derived class

  ```C+++
  class MotorHome : public Car, public Home 
  {
  	private:// Additional private members here
  	protected:// Additional protected members here
  	public:// Additional public members here
  };
  class MotorHome:public Car, protected Home
  { . . . };
  class MotorHome : public Car, Home // default: private Home
  { . . . };
  ```

  类`car`和`Home`也可以是`derived class`。

* ambiguity

  如果类`car`和`Home`是`derived class`，其`base class`相同，将会导致错误，产生歧义。若要解决这种歧义，可以使用范围解析运算符来确定要使用的基类。

  ```C++
  cout << motorHome.Home::getNr();
  ```

* virtual base class

  ```C++
  class PassCar : public virtual Car
  {// Here are additional members of class PassCar};
  class Van : public virtual Car{// Here are additional members of class Van};
  class SUV : public PassCar, public Van { . . . };
  ```

  可以定义仅包含间接基类的一个实例的多重派生类。多重派生类中的对象仅包含虚拟基类中成员的一个实例。这样可以确保多重继承类仅包含虚拟基类的一个实例。不能将间接基类的声明更改为`virtual`。

* initializing virtual base class

  * 虚拟基类的构造函数首先被调用，然后按照继承图中定义的顺序依次调用非虚拟基类的构造函数。
  * 虚拟基类的构造函数将使用为要派生的最后一个类（即继承图的最底端的类）的基本初始化方法声明的参数来调用。

  ```C++
  class SUV : public PassCar, public Van
  {
  	private:	// . . .
  	public:
  	SUV( ... ) : Car( ... )
  	{
  			// Initialize additional data members
  	}
  	void display() const
  	{
  	PassCar::display();
  	Van::display();		// Output additional data members
  	}
  };
  ```

---

# Chapter 28 Exception Handling 异常处理

* error handing

  传统的结构化编程语言使用常规语法来处理错误：

  * 函数调用中的错误由特殊的返回值指示。
  * 发生错误时设置全局错误变量或标志，然后在以后再次检查。

* exception handling

  异常处理（`exception handling`）基于将程序的正常功能与错误处理分开的基础。 基本思想是将在程序某个特定部分中发生的错误报告给程序的另一部分，称为调用环境。 调用环境执行中央错误处理。

  ```C++
  class Error
  {// Infos about the error cause
  };
  double calc( int a, int b )
  {
  	if ( b < 0 )
  		throw (string)"Denominator is negative!";
  	if( b == 0 )
  	{
  		Error errorObj;
  		throw errorObj;
  	}
  return ((double)a/b);
  }
  ```

* try and catch

  在实现异常处理时，需要指定两件事：

  * 程序中可能引发异常的部分。
  * 将处理各种异常类型的异常处理程序。

  通常，一个`try`块将包含一组可能产生类似错误的函数。每个`catch`块定义一个异常处理程序，其中用括号括起来的异常声明定义了该处理程序可以捕获的异常类型。通常的做法是为某些类型的错误定义特定的处理程序，为所有其他错误定义一个通用的处理程序。

  ```C++
  try
  {// Exceptions thrown by this block will be caught by the exception handlers, which are      //defined next.}
  catch( Type1 exc1)
  {// Type1 exceptions are handled here.}
  [ catch( Type2 exc2)
  {// Type2 exceptions are handled here.}
  . . . //etc.
  ]
  [ catch( ... )
  {
  // All other exceptions are handled here.
  }]
  ```

  当异常声明中的类型■与抛出的异常类型相同或■异常类型的基类或■基类指针并且异常是指向派生类的指针时，将调用处理程序。

* nesting exception handling

  一个`try`块可以包含其他`try`块。 这使您可以将嵌套`try`块中的处理程序用于特殊目的的错误处理，而将处理程序留在周围的`try`块中以处理剩余的错误。 嵌套`try`块中的处理程序还可以预先处理特定的错误，然后将控制权传递给`try`块包装器以进行最终处理。

  ```C++
  try
  {// Type1 exceptions are thrown here.
  	try
  	{// Type1 and Type2 exceptions are thrown here.}
  	catch( Type2 e2)
  	{// Type2 exceptions are pre-handled here
  		throw; // and thrown again.
  	}
  	// Other Type1 exceptions
  	// can be thrown.
  	}
  catch( Type1 e1)
  {// Type1 exceptions are handled here.}
  catch(...)
  {
  // All remaining exceptions are handled here,
  // particularly Type2 exceptions.
  }
  ```

* expection specification

  ```C++
  int func(int) throw(BadIndex, OutOfRange); // expections that func() can throw
  ```

  但是在C++11中异常声明已被弃用了，也就是不用`throw()`。

* standard exception specification

  `logic_error`用于表示由程序逻辑异常引起的逻辑错误。这些错误是可以避免的。
  `invalid_argument`,`out_of_range`,`length_error`,`domain_error`

  `runtime_error`用于表示运行时错误，例如内部计算中发生的不足或溢出。这些错误是不可预测的。

  `range_error`,`underflow_error`,`overflow_error`

  `what()`方法以C字符串形式返回此错误消息。

---

# Chapter 29 More about Files 文件拓展

[文件基础操作](# Chapter 18 Fundamentals of File Input and Output 文件输入和输出)

* random file access

  随机文件（`random file access`）访问使您可以选择在预定位置直接读取和写入信息。

  ```C++
  ios::openmode mode = ios::in | ios::out | ios::binary;
  fstream fstr("account.fle", mode);
  long rpos = myfile.tellg(); // get position of pointer
  ofstream fstr("account.fle", ios::out | ios::binary);
  fstr.seekp(pos, ios::begin);
  acc.write( fstr );		// write at the current position (pos)
  ```

  `ios::beg`，`ios::cur`，`ios::end`

  `tellp()`和`tellg()`方法以长值形式返回放置或获取指针的当前位置。

  可以使用`seekp()`或`seekg()`方法修改当前文件位置。该位置以相对于文件开头或结尾或相对于文件中当前位置的字节偏移量表示。

  可以将指针放置在文件末尾之后的位置，然后执行写操作，这将在文件中创建内容未知的间隙。 仅当文件中的所有空插槽长度相等时，这才有意义，因为以后可以覆盖它们。

  ```C++
  fstr.seekg(0L);			// set current position to the begining of file
  fstr.seekp(0L, ios::end); // set current position to the end of file
  unsigned long count = fstr.tellg(); // return the number of bytes occupied by the file
  ```

* state flags

  * `ios :: eofbit`到达文件末尾
  * `ios :: failbit`上次读取或写入操作失败
  * `ios :: badbit`发生了不可恢复的错误
  * `ios :: goodbit`流正常，例如 没有设置其他状态标志。

  `eof()`, `fail()`, `bad()`, and `good()` exists for each state flag

  `rdstate()`读取流的状态字

  ```C++
  if(myfile.rdstate() == ios::badbit) ...
  ```

  `clear()`方法可用于清除状态字，`clear(rdstate());`清除当前流的状态字

* exception handling

  可以使用`exceptions()`方法在流的状态字中指定将导致引发异常的标志。

  ```C++
  ifstream fstr("test.fle");
  fstr.exception(ios::failbit | ios::badbit);
  // call exception() without arguments
  iostate except = fstrm.exceptions();
  if( except & ios::eofbit) ...
  ```


---

# Chapter 30 More about Pointers 指针拓展

* pointer to pointers

  指针数组将被动态分配，或者函数期望指针数组作为参数。都需要声明一个指针变量，该变量可以访问数组中的第一个元素。 由于数组中的每个元素都是指针，因此该指针变量必须是指向指针的指针。

  ```C++
  Account** ptr = new Account*[400]; // generating pointer arrays dynamically
  *ptr and ptr[0] 			(pointer to index 0)
  *(ptr + i) and ptr[i]	 	(pointer to index i)
  **ptr and *ptr[0] 			(object addressed by pointer at index 0)
  **(ptr+i) and *ptr[i] 		(object addressed by pointer at index i)
  ```

* function with varying arguments

  C++允许定义允许可变数量的参数的函数，包括固定参数和可选参数。

  读取可选参数需要执行以下步骤：

  * 除其他局部变量之外，还必须声明`va_list`类型参数指针`argptr`。`va_list`类型在头文件`stdarg.h`。
  * 然后调用宏`va_start()`，将参数指针`argptr`指向第一个可选参数。 
  * 调用宏`va_arg()`时，将从堆栈中读取`argptr`指向的可选参数。
  * 在评估完参数之后，`va_end()`宏将参数指针设置为`NULL`。 

  ```C++
  #include <stdarg>
  int func(char* buffer, int max, ...)
  {
      va_list argp;
      va_start(argptr, max);
      va_arg(argp, int);
      va_end(argp);
  }
  ```

* pointer to function

  函数名称是指向该函数的常量指针。可以将许多函数保存在数组中以形成`jump table`，然后可以通过索引访问各个函数。

  ```C++
  bool compare(double, double); // Prototype
  bool (*funcptr)(double, double);
  funcptr = compare;
  (*funcptr)(9.1, 7.2);
  ```

* defining typenames

  使用`typedef`的主要优点是，它提高了程序的可读性，尤其是在命名复杂类型时。

  ```C++
  // 1st Example:
  typedef DayTime FREETIME;
  FREETIME timeArr[100];
  // 2nd Example:
  typedef struct { double re, im; } COMPLEX;
  COMPLEX z1, z2, *zp;
  // 3rd Example:
  typedef enum { Mo, Tu, We, Th, Fr } WORKDAY;
  WORKDAY day;
  // 4th Example:
  typedef enum { Diamonds, Hearts, Spades, Clubs } COLOR;
  typedef enum { seven, eight, nine, ten, jack, queen, king, ace } VALUE;
  typedef struct
  {
  	COLOR f;
  	VALUE w;
  } CARD;
  typedef CARD[10] HAND;
  HAND player1, player2, player3;
  ```

---

# Chapter 31 Manipulating Bits 操纵位

* bitwise operator

  逻辑：`& AND`与，`| inclusive OR`或，`^ exclusive OR`异或，`~ NOT`非

  转换：`<<`左转换，`>>`右转换

  按位运算符的操作数必须具有整数类型。

  区别：`ex1 && ex2`返回`false(boolean)`，`ex1 & ex2`返回`0(int,short,long)`。

  优先级：`~,(|,&,^),(&&,||)`

  移位运算符可以使用$2^{n}$执行高效的乘法和除法运算。向左（或向右）移动数字n位等效于乘以（或除以）$2^{n}$。

* bit mask

  `& AND`:deleting bits

  `| inclusive OR`:setting bits

  `^ exclusive OR`:inverting bits

  * `x & MASK`删除MASK中值为0的所有位。  
  * `x | MASK`设置MASK中值为1的所有位。
  * `x ^ MASK`反转MASK中值为0的所有位。

  `<<=,>>=,&=,^=,|=`

* bits-field

  位字段（`bits-field`）定义为类的数据成员。 每个位字段都是`unsigned int`类型，具有可选的名称和宽度。 宽度定义为位域在计算机字中所占的位数，并用冒号与位域名称分隔。

  ```C++
  struct { unsigned bit0_4 : 5;		// store 0-31
  		unsigned : 10;				// creat gap of 10 bits
  		unsigned bit15 : 1; } word;		// contain a value at position 15
  ```


---

# Chapter 32 Templates 模板

==函数模板==使用参数而不是具体类型为函数定义一组语句，==类模板==使用参数而不是具体类型来指定类定义。

优点：模板只需要编码一次。 必要时会自动生成单个函数或类。模板为类似问题提供了统一的解决方案，允许在开发阶段的早期对类型无关的代码进行测试。 避免了由多种编码引起的错误。

* define template

  模板的定义始终以`template <class T>`为前缀。

  ```C++
  template <class T>
  void exchange(T& x, T& y) // template function
  {
  	T help(x); x = y; y = help;
  }
  template <class U>
  class Demo				// template class
  {
  	U elem; . . . // etc.
  };
  typedef Demo<unsigned> UDemo; //use class Demo with type unsigned
  short a = 1, b = 7;
  exchange( a, b ); // instantiating (T = short) function
  Demo<int> elem(256); // instantiating class
  ```

* multiple template parameters

  ```C++
  template <class U, class V>
  class Demo
  { // . . . };
  bool Demo<U, V> method() {//...}
  ```

  除类型参数外，对模板参数有两个限制：无法修改和不能为浮点类型。

  除类型名称外，对模板参数还有一些限制：

  * 如果模板参数是引用，则只能将全局对象或静态对象作为模板参数传递。
  * 如果模板参数是指针，则仅对象或对象的地址 可以声明具有全局范围的函数。
  * 如果template参数既不是引用也不是指针，则只能将常量表达式用作模板参数。

  只有全局定义的字符串才能用于实例化，例如

  ```C++
  char str[] = "Oktoberfest"; // global
  Demo<double, str> income; 	// ok
  ```

* defining specialization

  如果模板函数被`specialization`替换，则在调用该函数时必须执行相应的版本。 编译器查找函数的顺序保证了，如果为特定类型定义了函数模板和`specialization`，则将优先调用`specialization`。

  ```C++
  template <class T>
  T Min(T x, T y) {return ((x < y) ? x : y);} // template function
  template<>
  const char* min( const char* s1, const char* s2 ) // specialization
  {return( (strcmp(s1, s2) < 0 ) ? s1: s2 );}
  ```

* default arguments of templates

  ```C++
  template <class T, int cnt = 10>
  class QuadMat
  {// ...};
  typedef QuadMat<> IntMat;
  IntMat m;	    // define a matrix m of int values
  typedef QuadMat<double> DoubleMat;
  DoubleMat dm;	// define a matrix m of double values
  ```

  * 如果至少为一个参数声明了默认实参，则必须为其余所有参数定义默认值。
  * 如果在实例化过程中省略了为其声明默认实参的模板实参，则必须省略所有剩余的模板实参。

  ```C++
  template class QuadMat<long double, 5>;
  int main()
  {
      QuadMat<long double, 5> m;
  	// ... 
  }
  ```

---

# Chapter 33 Containers 容器

`container`用于存储相同类型的对象，并提供管理这些对象的操作。这些操作包括对象插入、删除和检索。

顺序容器或序列，其中对象是按顺序排列的，对对象的访问可以是直接的或顺序的。

关联容器，其中对象通常以树结构组织和管理，并且可以使用键（`keys`）来引用。

## 33.1 Squence container 顺序容器

* squences

  下面是顺序容器（`squence container`）：

  * `arrays`数组，提供与C数组相同的操作，但与C数组相反，其大小动态地增加和减小。
  * `queues`队列，它们按FIFO（先进先出）原则进行管理。 
  * `stacks`堆栈，这些堆栈是按照LIFO（后进先出）原则进行管理的。

* associative container and bitsets

  关联容器包括

  * `sets`集合，允许通过可排序键快速访问对象
  * `maps`映射，保持有效对象/键对。

  也有所谓的位集（`bitsets`），它们代表给定长度的位序列，并提供按位运算符，可使用这些运算符来操作位。

* operation for squence

  <img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924110357027.png" alt="image-20200924110357027" style="zoom:80%;" />

* container adapters

  <img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924110450606.png" alt="image-20200924110450606" style="zoom:80%;" />

* squence and header files

  <img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924110534373.png" alt="image-20200924110534373" style="zoom:80%;" />

* iterators

  有两种类型的迭代器很重要：

  * 双向迭代器，可以由增量运算符`++`向上移动，由减量运算符`--`向下移动，并使用运算符`*`和`->`提供对对象的写入或读取访问 
  * 随机访问迭代器，它是可以额外执行随机定位的双向迭代器。 下标运算符`[]`为此被重载，并且定义了为指针算术定义的操作，例如整数的加/减或迭代器的比较。

* inserting methods

  <img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924115421052.png" alt="image-20200924115421052" style="zoom:80%;" />

  ```C++
  w.insert(--w.begin(), v.begin(), v.end()); //insert all objects in v into w at the beginning
  ```

  `adapter class`只有一种插入方法：`push()`。 在堆栈和队列中，`push()`向对象附加一个恒定的运行时。

* accessing objects
  * `front()`用于访问第一个元素。
  * `back()`用于访问最后一个元素。
  * `v[i]`和`v.at(i)`用于访问第`i+1`个元素。`v[i]`需要考虑是否超过数组范围。`list`没有定义该方式。

定义了`top()`方法以访问`adapter class`中的`priority_queue`和`stack`中具有最高优先级的元素或位于堆栈顶部的元素。`queen`类包含`front()`方法，该方法用于访问第一个元素。

* length and capacity

  `container`的标识特征是1.长度，即容器中保存的对象数。2.容量，即容器可以存储的最大对象数。

  ```C++
  Fraction x(1, 1);
  vector<Fraction> v(100, x);
  vector<Fraction>::size_type sz = v.size(); // size() get length
  while( !cont.empty() ) ... // empty() discover whether a container is empty
  cont.resize( n, x); // change lenth of a container to n, incerase n-size() copies of x
  size_type k = cont.max_size(); // max_size() discover the capacity of a container
  ```

* deletion methods

  * `pop_back()`删除`container`中的最后一个对象。
  * `delete()`删除给定位置上的对象，或删除给定范围内的所有对象。
  * `clear()`删除`container`中的所有对象。
  * `pop_front()`删除`container`中的第一个对象。不能用于`vector`。

  ```C++
  cont.erase(cont.begin() + 10, cont.end()); // delete objects starting at position 11
  wait.pop() // delete first element for adapter class
  ```

* list operators

  * `sort()`排序`list container`。
  * `reverse()`方法来反转`list container`，即，反转`container`中对象的顺序。
  * `merge()`方法用于合并两个`list container`。
  * `splice`拼接操作将一个`list container`中的对象插入到另一个`list container`中的给定位置，并将其从原始`container`中删除。可以转移整个`container`或仅转移一部分`container`。

## 33.2 Asscoiative container 关联容器

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924185521491.png" alt="image-20200924185521491" style="zoom: 80%;" />

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924185635288.png" alt="image-20200924185635288" style="zoom:80%;" />

<img src="C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20200924185635288.png" alt="image-20200924185635288" style="zoom:80%;" />

关联容器以所谓的堆`heap`（即最小高度的树）中的对象进行管理。堆的特征之一是具有最小密钥的对象始终存储在堆的顶部。映射`map`用于管理键/对象对。换句话说，密钥`key`没有嵌入对象中，而是与其分开存储。键的类型为Key，T为对象类型。对象之间的关系再次由键定义。

除了仅包含唯一键的映射外，您还可以定义多映射`multimap`，其中一个键可以存在多个对象。

定义了`begin()`和`end()`方法以访问所有关联容器类中的位置。

* sets and multisets

  ```C++
  typedef set<Account> AccountSet;
  AccountSet mySet(first, last);	// declaring sets and multisets
  mySet.insert(Account(1234,"May, Tom",100));	// insertion
  mySet.erase(mySet.begin());					// deletion
  mySet.erase(mySet.begin(), mySet.end());
  mySet.clear();	// clear all
  mySet.empty();  // whether container is empty or not
  mySet.size();   // return size of a container
  ```

* maps and multimaps

  C++标准库包含类模板对`<const Key，T>`，其中第一个和第二个具有两个公共数据成员，一个默认构造函数和一个表示键/对象对的复制构造函数。 第一个模板参数`Key`是键类型，第二个参数是对象类型`T`。数据成员首先用于存储键，其次用于存储关联的对象。
  
  用于插入的`insert()`方法，用于删除的`delete()`和`clear()`方法具有与容器类`set`和`multiset`中相同的接口。 还定义了可以用来发现容器长度的方法`size()`和确定容器是否为空的`empty()`方法。

  `find()`方法用于查找键/对象对，并期望键作为`map`和`multimap`类中的参数。 它的返回值是容器中的关联位置。 在`multimap`的情况下，多个对象可以具有相同的键，它将使用该键返回第一个位置。 如果搜索失败，则将值`end()`作为伪位置返回。

  可以使用`count()`方法发现容器中具有给定键的键/对象对的数量。该方法期望键作为参数。 该方法为映射返回0或1，这取决于是否存在一对。 当然，对于`multimap`，返回值可以大于1。

## 33.3 Bitset 

容器类`bitset <N>`提供管理位集所需的功能。模板参数`N`是位集的长度，即存储的最大位数。

位模式定义为无符号长值或字符串。

使用`get()`和`set()`方法读取和写入单个位。默认值为1。

`reset()`清除所有值，`flip()`使所有1变为0，使所有0变成1。

位运算符`&`，`|`和`^`在全局范围内过载。  NOT运算符`~`的运算符函数，移位运算符`<<`和`>>`以及复合赋值的运算符`&=`，`|=`，`^=`被实现为容器类的方法。



