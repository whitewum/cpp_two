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
