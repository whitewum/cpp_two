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

