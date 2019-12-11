# cpp_two
### 9.11 对6种创建和初始化vector对象的方法，每一种都给出一个实例。解释每个vector包含什么值。
答：
```
vector<int> vec;
vector<int> vec(10);    // 全为0
vector<int> vec(10,1);  // 全为1
vector<int> vec{1,2,3,4,5}; // 1,2,3,4,5
vector<int> vec(vec_0); // 与vec_0相同
vector<int> vec(vec_0.begin(), vec_0.end()); // 与vec_0相同
```
---
### 9.20 编写程序，从一个list< int >拷贝元素到两个deque中。值为偶数的所有元素都拷贝到一个deque中，而奇数值元素都拷贝到另一个deque中。
答：
```
#include<iostream>
#include<vector>
#include<list>
#include<deque>

int main()
{
    std::list<int> list0{1, 2, 3, 4, 5, 6, 7, 8, 9};
    std::deque<int> deque1;
    std::deque<int> deque2;
    std::list<int>::iterator it = list0.begin();
    for (it;it != list0.end();it++)
    {
        if (!((*it) % 2))
        {
            deque1.push_back(*it);
        }
        else
        {
            deque2.push_back(*it);
        }
    }
    std::cout << "偶数为：" << std::endl;
    for (std::deque<int>::iterator it = deque1.begin();it != deque1.end();it++)
    {
        std::cout << *it << ' ';
    }
    std::cout << std::endl << "奇数为" << std::endl;
    for (std::deque<int>::iterator it = deque2.begin();it != deque2.end();it++)
    {
        std::cout << *it << ' ';
    }
    return 0;
}
```
输出结果为：
>偶数为：
2 4 6 8
奇数为
1 3 5 7 9

---
### 9.29 假定vec包含25个元素，那么vec.resize(100)会做什么？如果接下来调用vec.resize(10)会做什么？
答：resize(100)会将vec的大小改变为100个元素的大小，添加新元素并且会默认初始化。接下来调用vec.resize(10)会将之后的90个元素舍弃，并且vec的大小变为10个元素的大小。

---
### 9.43 编写一个函数，接受三个string函数s、oldVal和newVal。使用迭代器及insert和erase函数将s中所有oldVal替换为newVal。测试你的程序，用它替换通用的简写形式，如，将"tho"替换为"though"，将"thru"替换为"through"。
答：
```
#include <iostream>
#include <string>

void func(std::string &s, std::string &oldVal, std::string &newVal);
int main()
{
    std::string s = "abcd thru through";
    std::string oldval = "thru";
    std::string newval = "through";
    func(s, oldval, newval);
    std::cout << s << std::endl;
    return 0;
}

void func(std::string &s, std::string &oldVal, std::string &newVal)
{
    std::string::iterator it = s.begin();
    while (it + oldVal.size() != s.end())
    {
        if (oldVal == std::string(it, it + oldVal.size()))
        {
            it = s.erase(it, it + oldVal.size());
            it = s.insert(it, newVal.begin(), newVal.end());
            std::advance(it ,newVal.size());
        }
        else
        {
            it++;
        }
    }
}
```
运行结果为：
>原语句："abcd thru through"
运行后语句："abcd through throuth"

---
### 9.52 使用stack处理括号化的表达式。当你看到一个左括号，将其记录下来。当你在一个左括号之后看到一个右括号，从stack中pop对象，直到遇到左括号，将左括号也一起弹出栈。然后将一个值（括号内运算结果）push到栈中，表示一个括号化的（子）表达式已经处理完毕，被其运算结果所取代。
答：
```
#include<iostream>
#include<stack>
#include<string>

bool isnum(char a)
{
    if (a >= '0' && a <= '9')
    {
        return true;
    }
    else
    {
        return false;
    }
}

int main()
{
    std::string expr("(1+2)+(3+4)+5");
    std::stack<char> st;
    int sum = 0;
    int len = expr.size();
    for (int i = 0; i < len; i++)
    {
        if (expr[i] == '(' || isnum((expr[i])))
        {
            st.push(expr[i]);
        }
        else if (expr[i] == '+')
        {
            continue;
        }
        else if (expr[i] == ')')
        {
            while (st.top() != '(')
            {
                sum += st.top() - '0';
                st.pop();
            }
            st.pop();
        }
    }
    while (!st.empty())
    {
        sum += st.top() - '0';
        st.pop();
    }
    std::cout << sum << std::endl;
    return 0;
}
```
>计算表达式为 (1+2)+(3+4)+5  
计算结果为 15

---

### 10.3 用accumulate求一个vector< int >中的元素之和。
答：
```
#include<iostream>
#include<numeric>
#include<vector>

int main() {
    std::vector<int> vec = { 1,2,3,4,5 };
    int sum = std::accumulate(vec.begin(), vec.end(), 0);
    std::cout << sum << std::endl;
    return 0;
}
```

### 10.15 编写一个lambda，捕获它所在的函数int，并接受一个int参数。lambda应该返回捕获的int和int参数的和。
答：
```
#include<iostream>

int main() {
    int a = 1;
    auto f = [a](int b) {return a + b;};
    std::cout << f(2) << std::endl; 
    return 0;
}
```

---

### 10.34 使用reverse_iterator逆序打印一个vector。
答：
```
#include <iostream>
#include <vector>

int main()
{
    std::vector<int> vec = {1, 2, 3, 4, 5};
    for (auto it = vec.rbegin(); it != vec.rend(); it++)
    {
        std::cout << *it << ' ';
    }
    return 0;
}
```
>原vec序列为1,2,3,4,5  
使用反向迭代器输出为5,4,3,2,1

---

### 10.42 使用list代替vector重新实现10.2.3节（第343页）中的去除重复单词的程序。
答：
```
#include <iostream>
#include <list>
#include <string>

int main()
{
    std::list<std::string> words = {"the", "quick", "red", "fox", "jumps", "over", "the", "slow", "red", "turtle"};
    words.sort();
    words.unique();
    for (auto i : words) {
        std::cout << i << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

---

### 11.12 编写程序，读入string和int的序列，将每个string和int存入一个pair中，pair保存在一个vector中。
答：
```
#include <iostream>
#include <string>
#include <vector>
#include <utility>

int main()
{
    std::vector<std::pair<std::string, int>> vec;
    std::string word;
    int i;
    std::cin >> word >> i;
    vec.push_back(std::pair<std::string, int>(word, i));
    std::cout << vec[0].first << ' ' << vec[0].second;
    return 0;
}
```

---

### 11.17 假定C是一个string的multiset，v是一个string的vector，解释下面的调用。指出每个调用是否合法。
答：
```
copy(v.begin(), v.end(), inserter(c, c.end())); 
// 将v中的元素拷贝到c中。使用合法，可以使用inserter将关联容器当作一个目的位置。
copy(v.begin(), v.end(), back_inserter(c));
// 意义同上，但是不合法，因为multiset没有push_back方法，不能调用back_inserter
copy(c.begin(), c.end(), inserter(v, v.end()));
// 将c中的元素拷贝到v中，使用合法，vector可以使用inserter。
copy(c.begin(), c.end(), back_inserter(v));
// 意义同上，合法，vector有push_back方法，可以使用back_inserter.
```

---

### 11.38 用unoredered_map重写单词计数程序（参见11.1节，第375页）和单词转换程序（参见11.3.6节，第391页）。
答：
```
#include <iostream>
#include <string>
#include <unordered_map>

int main()
{
    std::unordered_map<std::string, size_t> word_count;
    std::string word;
    while (std::cin >> word) {
        if (word == "Quit")
        {
            break;
        }
        ++word_count[word];
    }

    for (auto i : word_count) {
        std::cout << i.first << " occurs " << i.second << " times." << std::endl;
    }
}
```

---

### 13.12 在下面的代码片段中会发生几次折构函数调用？
答：
```
bool fcn (const Sales_data *trans, Sales_data accum)
{
    Sales_data item1 (*trans), item2 (accum);
    return item1.isbn() != item2.isbn();
}
```
>两次，退出作用域时，对item1, item2发生折构函数。

---

### 13.18 定义一个Employee类，它包含雇员的姓名和唯一的雇员证号。为这个类定义默认构造函数，以及接受一个表示雇员姓名的string的构造函数。每个构造函数应该通过一个static数据成员来生成一个唯一的证号。
```
class Employee
{
public:
    Employee () = default;
    Employee (const string& n) : name (n)
    {
        employee_id = ++increment_number;
    }

private:
    static int increment_number;
    int employee_id;
    string name;
};
```
### 13.46 什么类型的引用可以绑定到下面的初始化器上？
答：
```
int f();
vector<int> vi(100);
int? r1 = f();              // f()的返回值相当于一个常量，只能做右值引用或const引用，int &&r = f();
int? r2 = vi[0];            // 下标运算返回左值，所以应该用int &r = vi[0];
int? r3 = r1;               // r1此时相当与变量，int &r3 = r1;
int? r4 = vi[0] * f();       // 算术运算产生右值，int &&r4 = vi[0] * f();
```

---

### 13.49 为你的StrVec、String和Meggage类添加一个移动构造函数和一个移动赋值运算符。
答：
```
// Str.h文件中加：
StrVec (StrVec&& rhs) noexcept;
StrVec& operator= (StrVec&& rhs) noexcept;
// StrVec.cpp中加：
StrVec::StrVec(StrVec&& rhs) noexcept : elements (rhs.elements), first_free (rhs.first_free), cap (rhs.cap)
{
    rhs.elements = rhs.first_free = rhs.cap = nullptr;
}

StrVec& StrVec::operator=(StrVec&& rhs) noexcept
{
    if (this != &rhs) {
        free ();
        elements = rhs.elements;
        first_free = rhs.first_free;
        cap = rhs.cap;
        rhs.elements = rhs.first_free = rhs.cap = nullptr;
    }
    return *this;
}
```
```
//String.h
String (String&& s) noexcept;
String& operator= (String&& s) noexcept;
// String.cpp中加：
String::String(String&& s) noexcept : begin (s.begin), end (s.end)
{
    s.begin = s.end = nullptr;
}

String& String::operator= (String&& s) noexcept
{
    if (this != &s) {
        free();
        begin = s.begin;
        end = s.end;
        s.begin = s.end = nullptr;
    }
    return *this;
}
```
```
// Message.h
Message (Message&& m);
Message& operator= (Message&& m);
void moveFolders (Message* m);
// Message.cpp
void Message::moveFolders (Message* m)
{
    folders = std::move(m->folders);

    for (auto f : folders) {
        f->remMsg(m);
        f->addMsg(this);
    }
    m->folders.clear();
}

Message::Message (Message&& m) : contents (std::move(m.contents))
{
    moveFolders(&m);
}

Message& Message::operator=(Message&& m)
{
    if (this != &m) {
        remove_from_Folders();
        contents (std::move(m.contents));
        moveFolders(&m);
    }
    return *this;
}
```

---

### 13.58 编写新版本的Foo类，其sorted函数中有打印语句，测试这个类，来验证你对前两题的答案是否正确。
```
// .h文件
class Foo
{
public:
    Foo (std::vector<int>& ivec) : data(ivec) {}
    Foo sorted() &&;
    Foo sorted() const &;
    std::vector<int>& getData() { return data; }
private:
    std::vector<int> data;
};

.cpp文件
Foo Foo::sorted() &&
{
    sort(data.begin(), data.end());
    cout << "right value sorted." << endl;
    return *this;
}

Foo Foo::sorted() const &
{
    cout << "left value sorted." << endl;
    Foo ret (*this);
//    return ret.sorted();
    sort (ret.data.begin(), ret.data.end());
    return ret;
 //   return Foo(*this).sorted();
}

int main()
{
    vector<int> ivec = {1, 2, 5, 4, 7};
    Foo f1(ivec);
    Foo f2 = f1.sorted();

    for (auto i : f2.getData()) {
        cout << i << " ";
    }
    cout << endl;

    return 0;
}
```

---
### 14.3 















