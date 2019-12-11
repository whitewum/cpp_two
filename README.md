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



















