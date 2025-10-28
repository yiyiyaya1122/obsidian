
# 内存管理

- 栈区：内存由系统分配，大小固定，创建占用内存过大的局部变量会导致==栈溢出==。
- 堆区：比栈区大，内存需手动申请、释放，否则会导致==内存泄漏==。
# 常量

- 两种定义方式：1.宏常量 (#define Day 7)；2.const 修饰(const int day=7)
- 常量指针与指针常量
# 数据类型

- sizeof(int) or sizeof(value)
- short(2 bytes)、int(4 bytes)、long(4 bytes)、long long (8 bytes)
- float(4 bytes)  、 double(8 bytes)  ==float pi = 3.14f==   ==float f1 = 3e2==   ==float f2 = 3e-2==
- char(1 byte)：1.将对应的ASCII编码放入存储单元；2.不能用双引号创建；3.只能放入一个字符
- 转义字符：\\(输出\)、\n、\t
- 字符串：1.char 变量名[] = " " ；2. string (#include "string") 
- bool(1 byte)
- 数据输入：int a = 0; cin >> a ;
- 运算符
	- 算术运算符：`+、-、、/(整数相除结果为整数，小数部分省略)、%、++a(前置)、a++(后置)`
	- 赋值运算符：`=、+=、-=、*=、/=、%=`
	- 比较运算符：`== 、!=、<、>、<=、>=`
	- 逻辑运算符：` ! 、&&、|| `

# 程序流程结构

```cpp
// switch语句
// 优点：相比于if语句，结构清晰，执行效率高
// 缺点：不可以判断区间，表达式类型只能是整形或字符型；case里没有break会一直往下执行
int main()
{   
	int score = 10;
	switch (score)
	{
	case 10:
		cout << "good" << endl;
		break;
	case 9:
		cout << "not bad" << endl;
		break;
	case 8:
		cout << "just soso" << endl;
		break;
	default:
		cout << "default" << endl;
		break;
	}
}

// do...while...
int num = 1;
do
{
	cout<< num<<endl;
	num++;
}
while (num < 10);

// goto语句

int main() {
    int num;
    std::cout << "请输入一个大于 10 的整数: ";
    std::cin >> num;

    // 检查输入是否有效
    if (num <= 10) {
        // 若输入无效，跳转到 error 标签处
        goto error;
    }

    // 输入有效，进行正常处理
    std::cout << "你输入的数字是 " << num << "，满足要求。" << std::endl;
    // 跳转到 end 标签处结束程序
    goto end;

error:
    std::cout << "输入无效！请输入一个大于 10 的整数。" << std::endl;

end:
    std::cout << "程序结束。" << std::endl;
    return 0;
}    
```

#  数组

- 定义方式：`int arr[10]`、`int arr[5]={1,2,3,4,5}`、`int arr[] = {1,2,3,4}`
- 数组名用途：使用`sizeof(arr)/sizeof(arr[0])`计算数组长度；通过数组名查看数组首地址
- 元素逆置

```cpp
# 元素逆置
int arr[] = { 300, 350, 200, 400, 250 };

int left = 0;
int right = sizeof(arr) / sizeof(arr[0]) - 1;
int temp;

while (left < right)
{
	temp = arr[left];
	arr[left] = arr[right];
	arr[right] = temp;
	
	left += 1;
	right -= 1;
}

for (int i = 0; i < 5; i++)
{
	cout << arr[i] << endl;
}
```



