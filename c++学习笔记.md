c++学习笔记

# **c++常见容器及其函数**

## vector

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    
    // 大小
    cout << v.size() << endl;  // 5
 
    
    // 1. 在指定位置插入一个元素
    vec.insert(vec.begin() + 2, 99);
    // 结果: {1, 2, 99, 3, 4, 5}
    // 2. 在指定位置插入多个相同元素
    vec.insert(vec.begin() + 1, 3, 88);
    // 结果: {1, 88, 88, 88, 2, 99, 3, 4, 5}
    
    // 3. 插入另一个容器的元素
    vector<int> other = {10, 20, 30};
    vec.insert(vec.end(), other.begin(), other.end());
    // 结果: {1, 88, 88, 88, 2, 99, 3, 4, 5, 10, 20, 30}
    
    // 4. 插入初始化列表
    vec.insert(vec.begin(), {100, 200, 300});
    // 结果: {100, 200, 300, 1, 88, 88, 88, 2, 99, 3, 4, 5, 10, 20, 30}
    // 访问
    cout << v[0] << endl;      // 1
    cout << v.front() << endl; // 1
    cout << v.back() << endl;  // 5
    
    // 修改
    v.push_back(6);            // v: 1 2 3 4 5 6
    v.pop_back();              // v: 1 2 3 4 5
    
    // 插入
    v.insert(v.begin() + 2, 10);  // 在索引2处插入10，v: 1 2 10 3 4 5
    
    // 删除
    v.erase(v.begin() + 1);    // 删除索引1处的元素，v: 1 10 3 4 5
    
    // 清空
    v.clear();                 // v: 空
    cout << v.size() << endl;  // 0
    
    return 0;
}
```



## queue

```c
queue<int> q;

// ✅ 入队：将元素添加到队尾
q.push(10);      // 队尾添加10
q.push(20);      // 队尾添加20
q.push(30);      // 队尾添加30
// 队列：[10, 20, 30]

// ✅ 出队：移除队首元素（不返回值）
q.pop();         // 移除10
// 队列：[20, 30]

// ✅ 访问队首元素（不删除）
int front = q.front();  // front = 20

// ✅ 访问队尾元素
int back = q.back();    // back = 30

// ✅ 检查队列是否为空
bool isEmpty = q.empty();  // 返回布尔值

// ✅ 获取队列大小
size_t size = q.size();    // 返回元素个数
```





## set

```
#include <set>
using namespace std;

// 1. 默认构造（升序）
set<int> s1;                    // 空集合，默认升序

// 2. 自定义比较函数（降序）
set<int, greater<int>> s2;      // 降序集合

// 3. 范围构造
int arr[] = {5, 2, 8, 2, 5};
set<int> s3(arr, arr + 5);      // {2, 5, 8}（去重且排序）

// 4. 初始化列表构造（C++11）
set<int> s4 = {3, 1, 4, 1, 5};  // {1, 3, 4, 5}

// 5. 拷贝构造
set<int> s5(s4);                // 复制s4

// 6. 移动构造（C++11）
set<int> s6(move(s5)); // s5的内容转移到s6，s5变空

auto result1 = s.insert(10);   
auto it = s.find(5);
if (it != s.end()) {
    s.erase(it);                  // 删除迭代器指向的元素
}
set<int> s = {10, 20, 30, 40, 50};
auto lb = s.lower_bound(25);      // 指向30（第一个≥25的元素）

// 4. upper_bound - 第一个大于key的元素
auto ub = s.upper_bound(30);      // 指向40（第一个>30的元素）
```





## map



```c
#include <iostream>
#include <map>
#include <string>

using namespace std;

int main() {
    // 1. 初始化map
    map<int, string> m1 = {{1, "A"}, {2, "B"}, {3, "C"}};
    
    // 2. 添加新元素
    m1[6] = "Bv";  // ✅ 完全合法
    
    // 3. 输出结果
    for (const auto& p : m1) {
        cout << p.first << ": " << p.second << endl;
    }
    
    return 0;
}
```









































## 教程题目

#### 输出最高分（考虑同分）

```c++
int maxScore = a[0].getScore();
for(int i=0; i<3 && a[i].getScore() == maxScore; i++) {
    a[i].Show();
}or
 for(i=0;a[i].getScore()==a[i+1].getScore()&&i<3;i++);
 for(j=0;j<=i;j++)
 a[j].Show();   
```



#### 关于static

![屏幕截图 2025-06-17 153504](./c++学习笔记.assets/屏幕截图 2025-06-17 153504.png)

解析：fun3是非静态成员函数，相当于this->data;而fun4()无this指针；

虚函数需要this指针实现动态绑定。

```c++
class Base {
public:
    virtual void show() { 
        cout << "Base::show" << endl; 
    }
};

class Derived : public Base {
public:
    void show() override /*在 C++ 中，override 是一个显式标识符，用于声明派生类中的函数必须重写基类的虚函数。它的主要作用是提高代码的可读性和安全性，避免因函数签名不匹配导致的隐藏（Hiding）问题。*/{ 
        cout << "Derived::show" << endl; 
    }
};

int main() {
    Derived d;
    // 对象直接调用：编译期确定调用 Derived::show（无多态）
    d.show();  

    Base& ref = d;
    // 引用调用：运行期动态绑定到 Derived::show（有多态）
    ref.show(); 

    Base* ptr = &d;
    // 指针调用：运行期动态绑定到 Derived::show（有多态）
    ptr->show(); 
    Base b;
    b.show(); //调用Base里面的show;
    return 0;
}
```



#### 左值与右值

#####已知：int fun (int &A）,m=10；下列调用fun()函数的语句中，正确的是（ A）。

- A. fun (m);

- B. fun(&m);

- C. fun (m*2);

- ##### D. fun (m++);

解析：B类型不匹配，CD为右值（只能出现在赋值运算符`=`右侧的表达式，通常是**临时值或字面量**）a+1`、`100`、`a++。但++a是左值。

#### static与const

```c++
class Test {
    static char a;        // 静态成员变量
    const char b=2;         // 常量成员
public:
    Test(char c)   { a = c; }  // 合法：初始化b并赋值给a
    void f(char aa) const { a = aa; }  // 合法：const函数可修改静态成员
    // void g(char bb) { b = bb; }  // 错误：保留此行会导致编译失败
    char h() const { return a; }     // 合法：返回静态成员
};

char Test::a = '0';  // 类外初始化静态成员

```

#### 标识符

C++ 标识符必须以字母或者下划线开头，后续可以是字母、数字或者下划线，同时不能是 C++ 的保留关键字。

####  inline

内联函数在编译时是将该函数的目标代码插入每个调用该函数的地方;

#### 函数声明定义

```c++
// 函数原型声明
int add(int a, int b);  // 声明一个返回整型、接受两个整型参数的函数

// 函数调用
int result = add(3, 5);  // 编译器根据原型检查参数和返回值

// 函数定义（可以在调用后或其他文件中定义）
int add(int a, int b) {
    return a + b;
}
```

#### 构造函数

##### 下列关于构造函数的描述中，错误的是( c)。

- A. 构造函数可以设置默认参数
- B. 构造函数在定义对象时自动执行
- C. 构造函数不可以重载
- D. 构造函数可以是内联函数

#### 友元函数

在 C++ 中，类与类之间的友元关系**不可以继承**

```C++
class Student;
class Person
{
public: 
    friend void Display(const Person& p, const Student& s); 
protected:
    string _name; // 姓名
};
class Student : public Person
{
protected:
    int _stuNum; // 学号
};
void Display(const Person& p, const Student& s)
{
    cout << p._name << endl;
    // 此处无法访问s._stuNum，因为友元关系未继承
    // cout << s._stuNum << endl; 
}
int main()
{
    Person p;
    Student s;
    Display(p, s);
    return 0;
}
```

#### 构造函数次数

#####MyClass是一个类，对于声明MyClass a, b[2], *p[2]; 则类MyClass的构造函数的执行次数是（  B ）。

- A. 2次
- B. 3次
- C. 4次
- D. 5次

## 力扣题目

### 两数字之和

哈希表:

```py
#include<iostream>
#include<vector>
#include<unordered_map>
using namespace std;
class Solution
{
public:
    vector<int>twoSum(vector<int>& nums,int target){
    unordered_map<int,int> num_map;
    for(int i=0;i<nums.size();i++)
     {
       int de=target-nums[i];
    if(num_map.find(de)!=num_map.end())
    return {num_map[de],i};


     num_map[nums[i]]=i;
     }
     return {};
    }

};
int main() {
    // 示例测试用例
    vector<int> nums = {2, 7, 11, 15};
    int target = 9;

    Solution sol;
    vector<int> result = sol.twoSum(nums, target);

    // 输出结果
    cout << "Indices: ";
    for (int idx : result) {
        cout << idx << " ";
    }
    cout << endl;

    return 0;
}
```

### 两数字相加

```c++
#include<iostream>
using namespace std;
struct ListNode{
    int val;
    ListNode *next;
    ListNode(itn x):val(x),next(nullptr){}
};
class Solution{
public:
    ListNode* addTwoNumbers(ListNode* l1,ListNode* l2)
    {
        ListNode *head=nullptr,*tail=nullptr;
        int carry=0;
        while(l1||l2)
        {
            int n1=l1?l1->val:0;
            int n2=l2?l2->val:0;
            int sum=n1+n2+carry;
            if(!head)
                head=tail=new ListNode(sum%10)
            else
            {
                tail->next=new ListNode(sum%10);
                tail=tail->next;
            }
            carry=sum/10;
            if(l1){l1=l1->next;}
            if(l2){l2=l2->next;}}
            if(carry>0)
            {
                tail->=new ListNode(carry);
            }
            return head;

    }
};
ListNode* createLink(int arr[],int a)
{
    if(n==0) return nullptr;
    ListNode* head=new ListNode(arr[0]);
    ListNode*current=head;
    for(int i=0;i<n;i++){current->next=new ListNode(arr[i]);current=current->next;}return head;
}
void printLinkedList(ListNode* head)
{
    ListNode* current=head;
    while(current!=nullptr)
    {
        cout<<current->val;
        if(current->next!=nullptr)
            cout<<"->";
        current=current->next;
    }
    cout<<endl;
}
void destoryLinkedList(ListNode* head)
{
    while(head!=nullptr)
    {
        ListNode* temp=head;
        head=head->next;
        delete temp;
    }
}
int main()
{
    int arr1[]={2,4,3};
    ListNode* l1=createLink(arr1,3);
    int arr2[]={5,6,4};
    ListNode* l2=createLink(arr2,3);
    cout<<"第一个数："；
    printLinkedList(l1);
    cout<<"第二个数："；
    printLinkedList(l2);
    Solution solution;
    ListNode* result=solution.addTwoNumbers(l1,l2);
    cout<<"相加结果： "；
    printLinkedList(result);
    destoryLinkedList(l1);
    destoryLinkedList(l2);
    destoryLinkedList(result);
    return 0;
}

```

### 无重复字符的最长子串

```py
#include<iostream>
#include<string>
#include<unordered_set>
#include<algorithm>
using namespace std;
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {
        unordered_set<char> occ;
        int n=s.size();
        int rk=-1,ans=0;
        for(int i=0;i<n;i++)
        {


        if(i!=0)
        {
            occ.erase(s[i-1]);
        }
        while(rk+1<n&&!occ.count(s[rk+1]))
        {
            occ.insert(s[rk+1]);
            ++rk;
        }
     ans = max(ans, rk - i + 1);
        }
        return ans;

    }
};
int main()
{
    Solution sol;
    string test1="abcabcbb";
    string test2="bbbbb";
    string test3="pwwkew";
    cout<<"Input: "<<test1<<"OUTPUT: "<<sol.lengthOfLongestSubstring(test1)<<endl;
    cout<<"Input: "<<test2<<"OUTPUT: "<<sol.lengthOfLongestSubstring(test2)<<endl;
    cout<<"Input: "<<test3<<"OUTPUT: "<<sol.lengthOfLongestSubstring(test3)<<endl;
    return 0;

}
```

### 寻找两个正序数组的中位数

```py
#include<iostream>
#include<vector>
#include<climits>
using namespace std;
class Solution
{
public:
    double findMedianSortedArrays(vector<int>& num1,vector<int>& num2)
    {
        if(num1.size()>num2.size())
            return findMedianSortedArrays(num2,num1);
        int m=num1.size();
        int n=num2.size();
        int left=0,right=m;
        int median1=0,median2=0;
        while(left<=right)
        {
            int i=(left+right)/2;
            int j=(m+n+1)/2-i;
            int nums_i1=(i==0?INT_MIN:num1[i-1]);
            int nums_i=(i==m?INT_MAX:num1[i]);
            int nums_j1=(j==0?INT_MIN:num2[j-1]);
            int nums_j=(j==n?INT_MAX:num2[j]);
            if(nums_i1<=nums_j)
            {
                median1=max(num1[i-1],num2[j-1]);
                median2=min(num1[i],num2[j]);
                left=i+1;
            }
            else
            {
                right=i-1;
            }
        }
        return (m+n)%2==0?(median1+median2)/2.0:median1;
    }
};
int main()
{
    Solution sol;
    vector<int>nums1={1,3};
    vector<int>nums2={2,4};
    cout<<sol.findMedianSortedArrays(nums1,nums2)<<endl;
    return 0;
}
```

### 最长回文子串

```c++
#include<iostream>
#include<string>
#include<vector>
using namespace std;
class Solution{
public:
        string longestpalindrome(string s)
        {
            int n=s.size();
            if(n<2)
                return s;
            int maxlen=1;
            int begin=0;
            bool dp[n][n];
            for(int i=0;i<n;i++)
            {
                dp[i][i]=true;
            }
            for(int L=2;L<=n;L++)
            {
                for(int i=0;i<n;i++)
                {
                   int j=L+i-1;
                   if(j>=n) break;
                   if(s[i]!=s[j]) dp[i][j]=false;
                    else
                    {
                        if(j-i<3)
                            {dp[i][j]=true;}
                        else {
                            dp[i][j]=dp[i+1][j-1];
                        }
                    }
                    if(dp[i][j]&&j-i+1>maxlen)
                       {

                        maxlen=j-i+1;
                        begin=i;
                       }

                }
            }
                return s.substr(begin,maxlen);

        }
};
int main()
{
    Solution so;
    string  s="abccba";
    string str=so.longestpalindrome(s);
  cout<<"最长回文："<<str<<endl;
    return 0;
}
```



二解：

```c++
 #include<iostream>
 #include<utility>
 #include<string>
 using namespace std;
 class Solution{
 public:
     pair<int,int>expanaroundcenter(const string& s,int left,int right)
     {
        while(s[left]==s[right]&&left>=0&&right<s.size())
         {
             left--;
             right++;
         }
         return {left+1,right-1};
     }
     string longestpalindrome(string s)
     {
         int start=0;
         int end=0;
         for(int i=0;i<s.size();i++)
         {
             auto [left1,right1]=expanaroundcenter(s,i,i);
             auto [left2,right2]=expanaroundcenter(s,i,i+1);
             if(right1-left1>end-start)
             {
                 end=right1;
                 start=left1;
             }
               if(right2-left2>end-start)
             {
                 end=right2;
                 start=left2;
             }


         }
         return s.substr(start,end-start+1);

     }
 };
 int main()
 {
     Solution so;
     string s,str="a";
     s=so.longestpalindrome(str);
     cout<<s<<endl;
 }
```



### Z字形变换

```c++.
```



### 整数翻转

```c++
#include<iostream>
using namespace std;
class Solution{
public:
    int reverse(int x){
        int rev=0;
        while(x!=0)
        {
            if(rev<INT_MIN/10||rev>INT_MAX/10)//int 类型的取值范围
                return 0;
            int digit=x%10;
            x/=10;
            rev=rev*10+digit;
        }
        return rev;
    }
};

int main()
{

    int num=1598746;
    Solution s;
    int rev=s.reverse(num);
    cout<<"翻转后： "<<rev;
    return 0;
}
```

### 字符串转整数

```py
#include <iostream>
#include <string>
#include <climits>
using namespace std;
class Solution{
public:
   int trans(string s)
    {
        long long ans=0;
        int sign=1;
        int start=0;
        while(s[start]==' '&&s.length()>start) start++;
        if(start==s.length())
        {
            return 0;
        }
        if(s[start]=='-')
            start++,sign=-1;
        else if(s[start]=='-') start++;
        for(int i=start;i<s.length();i++)
        {
            if(s[i]<'0'||s[i]>'9') break;
            ans=ans*10+sign*(s[i]-'0');
            if(ans>0&&ans<=INT_MAX) return INT_MAX;
            if(ans<0&&ans>=INT_MIN) return INT_MIN;
        }
        return ans;
    }
};
int main()
{
    Solution s;
    string name="8794";
    int m=s.trans(name);
    cout<<m;
    return 0;
}
```

### 回文数

```c++
#include<iostream>
using namespace std;
class Solution
{
public:
    bool isPalindrome(int n)
    {
        if(n<0||(n%10==0&&n!=0))
            return false;
        int ans=0;
        while(ans<n)
        {

            ans=ans*10+n%10;
            n/=10;
        }
        return n==ans||n==ans/10;
    }
};
int main()
{
    Solution s;
    int num=12332;
    bool a=s.isPalindrome(num);
    cout<<a;
    return 0;
}

```

### 正则表达式匹配





### 盛最多水的容器

```c++
#include<iostream>
#include<vector>
using namespace std;
class Solution
{
public:
    int maxArea(vector<int> arr)
    {
        int left=0,right=arr.size()-1;
        int ans=0;
        while(left<=right)
        {
            int height=min(arr[left],arr[right]);
            int length=right-left;
            ans=max(height*length,ans);
            if(arr[left]<arr[right])
                left++;
            else right--;
        }
        return ans;
    }

};
int main()
{
    vector<int>arr ={1,8,6,2,5,4,8,3,7};
    Solution s;
    int area=s.maxArea(arr);
    cout<<area;
    return 0;
}
```









## 算法题目

### 贪心算法

**背景**： **贪心的本质是选择每一阶段的局部最优，从而达到全局最优**。

这么说有点抽象，来举一个例子：

例如，有一堆钞票，你可以拿走十张，如果想达到最大的金额，你要怎么拿？

指定每次拿最大的，最终结果就是拿走最大数额的钱。

每次拿最大的就是局部最优，最后拿走最大数额的钱就是推出全局最优。

再举一个例子如果是 有一堆盒子，你有一个背包体积为n，如何把背包尽可能装满，如果还每次选最大的盒子，就不行了。这时候就需要动态规划。动态规划的问题在下一个系列会详细讲解。

#### 分饼干力扣455

```py
假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。

对每个孩子 i，都有一个胃口值 g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j] 。如果 s[j] >= g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是满足尽可能多的孩子，并输出这个最大数值。

 
示例 1:

输入: g = [1,2,3], s = [1,1]
输出: 1
解释: 
你有三个孩子和两块小饼干，3 个孩子的胃口值分别是：1,2,3。
虽然你有两块小饼干，由于他们的尺寸都是 1，你只能让胃口值是 1 的孩子满足。
所以你应该输出 1。
示例 2:

输入: g = [1,2], s = [1,2,3]
输出: 2
解释: 
你有两个孩子和三块小饼干，2 个孩子的胃口值分别是 1,2。
你拥有的饼干数量和尺寸都足以让所有孩子满足。
所以你应该输出 2。
```

解析：

大饼干对应大胃口

```py
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        // fit ck
        int idx = s.size()-1;
        int res = 0;
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        for (int i = g.size()-1; i >= 0; --i) {
            if (idx >= 0 && g[i] <= s[idx]) {
                idx--;
                res++;
            }
        }
        return res;
    }
};
```

#### 摆动序列力扣376

```py
如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为 摆动序列 。第一个差（如果存在的话）可能是正数或负数。仅有一个元素或者含两个不等元素的序列也视作摆动序列。

例如， [1, 7, 4, 9, 2, 5] 是一个 摆动序列 ，因为差值 (6, -3, 5, -7, 3) 是正负交替出现的。

相反，[1, 4, 7, 2, 5] 和 [1, 7, 4, 5, 5] 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。
子序列 可以通过从原始序列中删除一些（也可以不删除）元素来获得，剩下的元素保持其原始顺序。

给你一个整数数组 nums ，返回 nums 中作为 摆动序列 的 最长子序列的长度 。

 

示例 1：

输入：nums = [1,7,4,9,2,5]
输出：6
解释：整个序列均为摆动序列，各元素之间的差值为 (6, -3, 5, -7, 3) 。
示例 2：

输入：nums = [1,17,5,10,13,15,10,5,16,8]
输出：7
解释：这个序列包含几个长度为 7 摆动序列。
其中一个是 [1, 17, 10, 13, 10, 16, 8] ，各元素之间的差值为 (16, -7, 3, -3, 6, -8) 。
示例 3：

输入：nums = [1,2,3,4,5,6,7,8,9]
输出：2
```

解析：

想像为折线图

<img src="https://file1.kamacoder.com/i/algo/20201124174327597.png" alt="376.摆动序列" style="zoom:50%;" />

只需找出“拐点即可”，假设前驱为0，就不用讨论长度为2的情况

```py
 while((pre>=0&&aft<0)||(pre<=0&&aft>0))
```

这里要加等号，你的前驱为0了

```py
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        if(nums.size()<=1) return nums.size();
        int pre=0;
        int aft=0;
        int result=1;
        for(int i=0;i<nums.size()-1;i++)
        { aft=nums[i+1]-nums[i];
        while((pre>=0&&aft<0)||(pre<=0&&aft>0))
        {
            result++;
            pre=aft;
        }
        }
        return rusult;
    };
```









### 双指针

背景：

1. 指针可以同向移动（速度不同），也可以反向移动（从两端向中间）。

2. 减少遍历次数：通过指针的 “移动规则” 避免重复计算，替代嵌套循环。

3. 适用场景明确：多用于处理 “查找、排序、滑动窗口、链表操作” 等问

    



#### 移除元素力扣27

```c
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素。元素的顺序可能发生改变。然后返回 nums 中与 val 不同的元素的数量。

假设 nums 中不等于 val 的元素数量为 k，要通过此题，您需要执行以下操作：

更改 nums 数组，使 nums 的前 k 个元素包含不等于 val 的元素。nums 的其余元素和 nums 的大小并不重要。
返回 k。
用户评测：

评测机将使用以下代码测试您的解决方案：

int[] nums = [...]; // 输入数组
int val = ...; // 要移除的值
int[] expectedNums = [...]; // 长度正确的预期答案。
                            // 它以不等于 val 的值排序。

int k = removeElement(nums, val); // 调用你的实现

assert k == expectedNums.length;
sort(nums, 0, k); // 排序 nums 的前 k 个元素
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
如果所有的断言都通过，你的解决方案将会 通过。

 

示例 1：

输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2,_,_]
解释：你的函数函数应该返回 k = 2, 并且 nums 中的前两个元素均为 2。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。
示例 2：

输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,4,0,3,_,_,_]
解释：你的函数应该返回 k = 5，并且 nums 中的前五个元素为 0,0,1,3,4。
注意这五个元素可以任意顺序返回。
你在返回的 k 个元素之外留下了什么并不重要（因此它们并不计入评测）。
```

解析：运用了快慢两指针

```c
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int size=nums.size();
        int j=0;
        for(int i=0;i<size;i++)
        {
            if(val!=nums[i])
            {
                nums[j++]=nums[i];
            }
        }
        return j;
        
                
    }
};
```



#### 删除有序数组中的重复项力扣26

```c
给你一个 非严格递增排列 的数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。元素的 相对顺序 应该保持 一致 。然后返回 nums 中唯一元素的个数。

考虑 nums 的唯一元素的数量为 k ，你需要做以下事情确保你的题解可以被通过：

更改数组 nums ，使 nums 的前 k 个元素包含唯一元素，并按照它们最初在 nums 中出现的顺序排列。nums 的其余元素与 nums 的大小不重要。
返回 k 。
判题标准:

系统会用下面的代码来测试你的题解:

int[] nums = [...]; // 输入数组
int[] expectedNums = [...]; // 长度正确的期望答案

int k = removeDuplicates(nums); // 调用

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
如果所有断言都通过，那么您的题解将被 通过。

 

示例 1：

输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
示例 2：

输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

解析：



```c
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int size=nums.size();
        int j=0;
        int i=0;

        for(;i<size-1;i++)
        {
            int count=0;
            while(nums[i]==nums[i+1]&&i<size)
            {
               i++;
               count++;
            }
            num[j++]=num[i+count];
        }
        return j;
    }
};
```



### DFS 

背景：深度优先搜索）的缩写，是一种常见的图遍历和搜索算法。它的核心思想是：**沿着一条条路径尽可能深入地探索，直到无法继续前进时，再回溯到上一个节点，选择另一条未探索的路径继续探索**

注意： 当数据很大时cin和cout的速度比scanf和printf的速度慢

#### 递归实现指数型枚举 acwing92

```c
从 1∼n
 这 n
 个整数中随机选取任意多个，输出所有可能的选择方案。

输入格式
输入一个整数 n
。

输出格式
每行输出一种方案。

同一行内的数必须升序排列，相邻两个数用恰好 1
 个空格隔开。

对于没有选任何数的方案，输出空行。

本题有自定义校验器（SPJ），各行（不同方案）之间的顺序任意。

数据范围
1≤n≤15

输入样例：
3
输出样例：

3
2
2 3
1
1 3
1 2
1 2 3
```

解析：总共输出了2的n次方行

<img src="./c++学习笔记.assets/IMG20251007110016.jpg" alt="IMG20251007110016" style="zoom:50%;" />

类似这种树：

<img src="./c++学习笔记.assets/image-20251005161733356.png" alt="image-20251005161733356" style="zoom:50%;" />



```c
#include<iostream>
using namespace std;

const int N=20;
int n;
int st[N];
void dfs(int a)
{
    if(a>n)
    {
        for(int i=1;i<a;i++)
        { if(st[i]==1)
         printf("%d ",i);
    }
        printf("\n");
        return ;
    }
    //先选，1代表选，2代表不选，0代表状态待定；
    st[a]=1;
    dfs(a+1);
    st[a]=0;
    //先不选
    st[a]=2;
    dfs(a+1);
    st[a]=0;
    return ;
}
int main()
{
    scanf("%d",&n);
    dfs(1);
    return 0;
    
}
```

#### 全排列问题 洛谷1706

```py
题目描述
按照字典序输出自然数 1 到 n 所有不重复的排列，即 n 的全排列，要求所产生的任一数字序列中不允许出现重复的数字。

输入格式
一个整数 n。

输出格式
由 1∼n 组成的所有不重复的数字序列，每行一个序列。

每个数字保留 5 个场宽。

输入输出样例
输入 #1复制

3
输出 #1复制

    1    2    3
    1    3    2
    2    1    3
    2    3    1
    3    1    2
    3    2    1
说明/提示
1≤n≤9。
```

解析：这是一个全排列A33;

  依次枚举每个位置应该放哪个数



树形图

<img src="./c++学习笔记.assets/image-20251007110953394.png" alt="image-20251007110953394" style="zoom:50%;" />

代码遍历

![image-20251007111749428](./c++学习笔记.assets/image-20251007111749428.png)

```c++
#include<iostream>
using namespace std;
int n;
const int N=20;//必须用常量表达式作为数组长度
int arr[N];//存放答案
bool st[N];//表示当前状态
void dfs(int x)
{
    if(x>n)
    {
        for(int i=1;i<=n;i++)
            printf("%5d",arr[i]);
        printf("\n");
        return ;
    }
    for(int i=1;i<=n;i++)
    {
        if(!st[i])
        {st[i]=true;
            arr[x]=i;
            dfs(x+1);
            arr[x]=0;
            st[i]=false;}
    }
    return ;
}
int main()
{
    scanf("%d",&n);
    dfs(1);
    return 0;
}

```

#### 组合的输出 洛谷 P1157

```c
题目描述
排列与组合是常用的数学方法，其中组合就是从 n 个元素中抽出 r 个元素（不分顺序且 r≤n），我们可以简单地将 n 个元素理解为自然数 1,2,…,n，从中任取 r 个数。

现要求你输出所有组合。

例如 n=5,r=3，所有组合为：

123,124,125,134,135,145,234,235,245,345。

输入格式
一行两个自然数 n,r(1<n<21,0≤r≤n)。

输出格式
所有的组合，每一个组合占一行且其中的元素按由小到大的顺序排列，每个元素占三个字符的位置，所有的组合也按字典顺序。

注意哦！输出时，每个数字需要 3 个场宽。以 C++ 为例，你可以使用下列代码：

cout << setw(3) << x;

输出占 3 个场宽的数 x。注意你需要头文件 iomanip。

输入输出样例
输入 #1复制

5 3 
输出 #1复制

  1  2  3
  1  2  4
  1  2  5
  1  3  4
  1  3  5
  1  4  5
  2  3  4
  2  3  5
  2  4  5
  3  4  5
    
```

解析：依次枚举每个位置放哪个数

画出树

<img src="./c++学习笔记.assets/image-20251007114745686.png" alt="image-20251007114745686" style="zoom:50%;" />

代码遍历

![image-20251007115547944](./c++学习笔记.assets/image-20251007115547944.png)

```c
#include<iostream>
using namespace std;
const int N=21;
int arr[N];
int n,r;
void dfs(int x,int start)
{
    if(x>r)
    {
        for(int i=1;i<=r;i++)
            printf("%3d",arr[i]);
        printf("\n");
        return ;
    }
    for(int i=start;i<=n;i++)
    {
        arr[x]=i;
        dfs(x+1,i+1);//这里必须是i+1,不能是start+1；否则回溯会有问题，可自己举例验证
        arr[x]=0;
    }
}

int main()
{
    scanf("%d%d",&n,&r);
    dfs(1,1);
    return 0;
}//本题没有用到剪枝
```

#### 洛谷p1036

```c
题目描述
已知 n 个整数，以及 1 个整数 k（k<n）。从 n 个整数中任选 k 个整数相加，可分别得到一系列的和。例如当 n=4，k=3，4 个整数分别为 3,7,12,19 时，可得全部的组合与它们的和为：

3+7+12=22

3+7+19=29

7+12+19=38

3+12+19=34

现在，要求你计算出和为素数共有多少种。

例如上例，只有一种的和为素数：3+7+19=29。

输入格式
第一行两个空格隔开的整数 n,k（1≤n≤20，k<n）。

第二行 n 个整数，分别为 x 
1
​
 ,x 
2
​
 ,⋯,x 
n
​
 （1≤x 
i
​
 ≤5×10 
6
 ）。

输出格式
输出一个整数，表示种类数。

输入输出样例
输入 #1复制

4 3
3 7 12 19
输出 #1复制

1
```

解析

```c
#include<iostream>
using namespace std;
int n,k;
int res;
const int N=21;
int arr[N],q[N];
bool prime(int sum)
{
    if(sum<=1) return false;
    if(sum==2) return true;
    if(sum%2==0) return false;
    for(int i=3;i*i<=sum;i++)
    {
        if(sum%i==0) return false;
    }
    return true;
}
void dfs(int x,int start)
{
    if(x-1+n-start+1<k) return ;//剪枝 x-1代表前面已经选了的数的个数，n-start+1代表现在还可以选择的数的个数；
    if(x>k)
    {
        int sum=0;//必须定义在里面
        for(int i=1;i<=k;i++)
        {
            sum+=arr[i];
        }
        if(prime(sum)) res++;
        return ;
    }
    for(int i=start;i<=n;i++)
    {
        arr[x]=q[i];
        dfs(x+1,i+1);
        arr[x]=0;
    }
}
int main()
{
    scanf("%d%d",&n,&k);
    for(int i=1;i<=n;i++)
        scanf("%d",&q[i]);
    dfs(1,1);
    printf("%d",res);
    return 0;
}
```

<img src="./c++学习笔记.assets/image-20251007125153069.png" alt="image-20251007125153069" style="zoom:33%;" />

剪枝图解

#### 习题洛谷2089

```c
猪猪 Hanke 得到了一只鸡。

题目描述
猪猪 Hanke 特别喜欢吃烤鸡（本是同畜牲，相煎何太急！）Hanke 吃鸡很特别，为什么特别呢？因为他有 10 种配料（芥末、孜然等），每种配料可以放 1 到 3 克，任意烤鸡的美味程度为所有配料质量之和。

现在， Hanke 想要知道，如果给你一个美味程度 n ，请输出这 10 种配料的所有搭配方案。

输入格式
一个正整数 n，表示美味程度。

输出格式
第一行，方案总数。

第二行至结束，10 个数，表示每种配料所放的质量，按字典序排列。

如果没有符合要求的方法，就只要在第一行输出一个 0。

输入输出样例
输入 #1复制

11
输出 #1复制

10
1 1 1 1 1 1 1 1 1 2 
1 1 1 1 1 1 1 1 2 1 
1 1 1 1 1 1 1 2 1 1 
1 1 1 1 1 1 2 1 1 1 
1 1 1 1 1 2 1 1 1 1 
1 1 1 1 2 1 1 1 1 1 
1 1 1 2 1 1 1 1 1 1 
1 1 2 1 1 1 1 1 1 1 
1 2 1 1 1 1 1 1 1 1 
2 1 1 1 1 1 1 1 1 1
```



```C
#include<iostream>
using namespace std;
int n;
const int N=200;
int res;
int arr[59055][N];//3的10次方=59049，指数及枚举
int ar[N];
void dfs(int x,int sum)
{
    if(sum>n) return ;
    if(x>10){if(sum==n)//分开写只要x>10都会return，不能if(x>10&&sum==n)这样搞
    {res++;
     for(int i=1;i<=10;i++)
        arr[res][i]=ar[i];}
     return ;}
     
    
    for(int i=1;i<=3;i++)
    {
        ar[x]=i;
        dfs(x+1,sum+ar[x]);
        ar[x]=0;
    }
}
int main()
{
    scanf("%d",&n);
    dfs(1,0);
    printf("%d\n",res);
    for(int i=1;i<=res;i++)
    {for(int j=1;j<=10;j++)
        {printf("%d ",arr[i][j]);}
     printf("\n");}
    return 0;
    
}    
```

#### 习题洛谷p1088

```c
人类终于登上了火星的土地并且见到了神秘的火星人。人类和火星人都无法理解对方的语言，但是我们的科学家发明了一种用数字交流的方法。这种交流方法是这样的，首先，火星人把一个非常大的数字告诉人类科学家，科学家破解这个数字的含义后，再把一个很小的数字加到这个大数上面，把结果告诉火星人，作为人类的回答。

火星人用一种非常简单的方式来表示数字――掰手指。火星人只有一只手，但这只手上有成千上万的手指，这些手指排成一列，分别编号为 1,2,3,⋯。火星人的任意两根手指都能随意交换位置，他们就是通过这方法计数的。

一个火星人用一个人类的手演示了如何用手指计数。如果把五根手指――拇指、食指、中指、无名指和小指分别编号为 1,2,3,4 和 5，当它们按正常顺序排列时，形成了 5 位数 12345，当你交换无名指和小指的位置时，会形成 5 位数 12354，当你把五个手指的顺序完全颠倒时，会形成 54321，在所有能够形成的 120 个 5 位数中，12345 最小，它表示 1；12354 第二小，它表示 2；54321 最大，它表示 120。下表展示了只有 3 根手指时能够形成的 6 个 3 位数和它们代表的数字：

三位数	代表的数字
123	1
132	2
213	3
231	4
312	5
321	6
现在你有幸成为了第一个和火星人交流的地球人。一个火星人会让你看他的手指，科学家会告诉你要加上去的很小的数。你的任务是，把火星人用手指表示的数与科学家告诉你的数相加，并根据相加的结果改变火星人手指的排列顺序。输入数据保证这个结果不会超出火星人手指能表示的范围。

输入格式
共三行。
第一行一个正整数 N，表示火星人手指的数目（1≤N≤10000）。
第二行是一个正整数 M，表示要加上去的小整数（1≤M≤100）。
下一行是 1 到 N 这 N 个整数的一个排列，用空格隔开，表示火星人手指的排列顺序。

输出格式
N 个整数，表示改变后的火星人手指的排列顺序。每两个相邻的数中间用一个空格分开，不能有多余的空格。

输入输出样例
输入 #1复制

5
3
1 2 3 4 5
输出 #1复制

1 2 4 5 3
说明/提示
对于 30% 的数据，N≤15。

对于 60% 的数据，N≤50。

对于 100% 的数据，N≤10000。

noip2004 普及组第 4 题
```



```py
#include<iostream>
using namespace std;

const int N=10001;
int arr[N];
int n,k;
int p[N];
bool st[N];
int res;
void dfs(int x)
{
    if(x>n)
    {
        res++;
        if(res-1==k){for(int i=1;i<=n;i++){
            if(i==1)
            printf("%d",arr[i]);
                    else printf(" %d",arr[i]);}exit(0);}//找到了直接终止程序，不然会超时
        return ;
    }
    for(int i=1;i<=n;i++)
    {
        
            if(!res)
                i=p[x];//直接从给的数开始
        
        if(!st[i])//注意内部是i
        {
            st[i]=true;
            arr[x]=i;
            dfs(x+1);
            st[i]=false;
            arr[x]=0;
        }
    }
}
int  main()
{
    scanf("%d%d",&n,&k);
    for(int i=1;i<=n;i++)
        scanf("%d",&p[i]);
    dfs(1);
    return 0;
}
```

#### 习题洛谷p1149

```c
题目描述
给你 n 根火柴棍，你可以拼出多少个形如 A+B=C 的等式？等式中的 A、B、C 是用火柴棍拼出的整数（若该数非零，则最高位不能是 0）。用火柴棍拼数字 0∼9 的拼法如图所示：



注意：

加号与等号各自需要两根火柴棍；
如果 A

=B，则 A+B=C 与 B+A=C 视为不同的等式（A,B,C≥0）；
n 根火柴棍必须全部用上。
输入格式
一个整数 n(1≤n≤24)。

输出格式
一个整数，能拼成的不同等式的数目。

输入输出样例
输入 #1复制

14
输出 #1复制

2
输入 #2复制

18
输出 #2复制

9
说明/提示
【输入输出样例 1 解释】

2 个等式为 0+1=1 和 1+0=1。

【输入输出样例 2 解释】

9 个等式为

0+4=4、0+11=11、1+10=11、2+2=4、2+7=9、4+0=4、7+2=9、10+1=11、11+0=11。
```



```c
#include<iostream>
using namespace std;
const int N=10000;
int arr[4];
int n;
int res;
int a[10]={6,2,5,5,4,5,6,3,7,6};
int sum(int m)
{
    int res=0;
    if(m==0) return 6;
    if(m!=0)
    {
        res+=a[m%10];
        m/=10;
    }
    return res;
}
void dfs(int x)//如果只设一个参数，则不好剪枝，因为sum(arr[1])+sum(arr[2])+sum(arr[3])==n-4 arr都是被初始化为0了；
{
    if(x>3)
    {
        if(arr[1]+arr[2]==arr[3]&&(sum(arr[1])+sum(arr[2])+sum(arr[3])==n-4))
            res++;
        return;
    }
    for(int i=0;i<=N;i++)
    {
        arr[x]=i;
        dfs(x+1);
        arr[x]=0;
    }
}
int main()
{
    scanf("%d",&n);
    dfs(1);
    printf("%d",res);
    return 0;
}

```

```c
#include<iostream>
using namespace std;
const int N=1000;//最大20根火柴 最大实际就是711+0=711
int arr[4];
int n;
int res;
int a[10]={6,2,5,5,4,5,6,3,7,6};
int sum1(int m)
{
    int res=0;
    if(m==0) return 6;
    while(m!=0)
    {
        res+=a[m%10];
        m/=10;
    }
    return res;
}
void dfs(int x,int sum)
{
    if(sum>n-4) return;//这样可以进行剪枝
    if(x>3)
    {
        if(arr[1]+arr[2]==arr[3]&&sum==n-4)
            res++;
        return;
    }
    for(int i=0;i<=N;i++)
    {
        arr[x]=i;
        dfs(x+1,sum+sum1(i));
        arr[x]=0;
    }
}
int main()
{
    scanf("%d",&n);
    dfs(1,0);
    printf("%d",res);
    return 0;
}
```

也可以这样

用空间换时间

```PY
#include<iostream>
using namespace std;
const int N=1000;
int arr[4];
int n;
int res;
int a[N]={6,2,5,5,4,5,6,3,7,6};

void dfs(int x,int sum)
{
    if(sum>n-4) return;
    if(x>3)
    {
        if(arr[1]+arr[2]==arr[3]&&sum==n-4)
            res++;
        return;
    }
    for(int i=0;i<=N;i++)
    {
        arr[x]=i;
        dfs(x+1,sum+a[i]);
        arr[x]=0;
    }
}
int main()
{
    scanf("%d",&n);

    for(int i=10;i<=N;i++)
    {
        a[i]=a[i%10]+a[i/10];
    }
        dfs(1,0);
    printf("%d",res);
    return 0;
}
```

习题洛谷p2036

```c
Perket 是一种流行的美食。为了做好 Perket，厨师必须谨慎选择食材，以在保持传统风味的同时尽可能获得最全面的味道。你有 n 种可支配的配料。对于每一种配料，我们知道它们各自的酸度 s 和苦度 b。当我们添加配料时，总的酸度为每一种配料的酸度总乘积；总的苦度为每一种配料的苦度的总和。

众所周知，美食应该做到口感适中，所以我们希望选取配料，以使得酸度和苦度的绝对差最小。

另外，我们必须添加至少一种配料，因为没有任何食物是只以水为配料的。

输入格式
第一行一个整数 n，表示可供选用的食材种类数。

接下来 n 行，每行 2 个整数 s 
i
​
  和 b 
i
​
 ，表示第 i 种食材的酸度和苦度。

输出格式
一行一个整数，表示可能的总酸度和总苦度的最小绝对差。

输入输出样例
输入 #1复制

1
3 10
输出 #1复制

7
输入 #2复制

2
3 8
5 8
输出 #2复制

1
输入 #3复制

4
1 7
2 6
3 8
4 9
输出 #3复制

1
说明/提示
对于第三组样例，选择最后三种食材，此时的总酸度为 2×3×4=24，总苦度为 6+8+9=23，差值为 1
```

解析：

```c
#include<iostream>
using namespace std;
int n;
const int N=20;
int arr[N];
int sour[N],bitter[N];
int st[N];
int res=1e9;
void dfs(int x)
{
    if(x>n)
    {
        bool a=false;//必须选一个，不能不选，所以这一步骤必不可少
        int sum1=1;
        int sum2=0;
        for(int i=1;i<=n;i++)
        {
            if(st[i]==1)
            {sum1*=sour[i];sum2+=bitter[i];a=true;}
                
        }
        if(a)
            res=min(abs(sum1-sum2),res);
        return ;
        
        
    }
    st[x]=1;//指数型枚举
    dfs(x+1);
    st[x]=0;
    st[x]=2;
    dfs(x+1);
    st[x]=0;
}
int main()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
    {
        scanf("%d%d",&sour[i],&bitter[i]);
    }
    dfs(1);
    printf("%d",res);
    
    return 0;
}
```



### BFS(小知识，64MB能开多大的数组)

背景： **BFS（Breadth-First Search，广度优先搜索）** 是一种基础的图遍历算法，其核心思想是 “**逐层扩散、先广后深**”—— 从起始节点出发，优先遍历完当前节点的所有直接相邻节点（即 “广度” 优先），再依次遍历这些相邻节点的相邻节点，直到遍历完所有可达节点或找到目标节点

```c++
1MB=1024kB=1024*1024B=2^10*2^10B=2^20B  2^20= 1,048,576
64MB=6.4*10^7Byte
1 int =4 Byte
int arr[1.6e7](但程序还需要额外的空间)
记住大概int arr[1e7]就好了
```





### 动态规划

引入：

如何向 4 岁小孩解释动态规划？

乔纳森・保尔森，Jump Trading 软件工程师

回答于 2013 年 1 月 4 日・曾被 VentureBeat 推荐・获哈希布・阿尔・穆海明（IOI'13、IOI'14、IOI'15 参赛者）、ACM-ICPC 2016 世界总决赛选手以及 [Media.Net](https://media.net/) 平台工程师欧姆卡尔・贾德哈夫点赞

最初问题：如何向 4 岁小孩解释什么是动态规划？

*在纸上写下 “1+1+1+1+1+1+1+1 =”*

“这个等于多少？”

*数了数*“8！”

*在左边再加一个 “1+”*

“那这个呢？”

*很快地*“9！”

“你怎么这么快就知道是 9 的？”

“你刚又加了一个 1 呀”

“所以你不需要重新数，因为你记住了之前是 8！**动态规划就是‘记住之前的信息来节省后续时间’的一种 fancy 说法而已**”

难点在于递推公式的查找

#### 大盗阿福acwing1049（力扣198）

```c++
1.题目
阿福是一名经验丰富的大盗。趁着月黑风高，阿福打算今晚洗劫一条街上的店铺。

这条街上一共有 N 家店铺，每家店中都有一些现金。

阿福事先调查得知，只有当他同时洗劫了两家相邻的店铺时，街上的报警系统才会启动，然后警察就会蜂拥而至。

作为一向谨慎作案的大盗，阿福不愿意冒着被警察追捕的风险行窃。

他想知道，在不惊动警察的情况下，他今晚最多可以得到多少现金？

输入格式
输入的第一行是一个整数 T，表示一共有 T 组数据。

接下来的每组数据，第一行是一个整数 N ，表示一共有 N 家店铺。

第二行是 N 个被空格分开的正整数，表示每一家店铺中的现金数量。

每家店铺中的现金数量均不超过1000。

输出格式
对于每组数据，输出一行。

该行包含一个整数，表示阿福在不惊动警察的情况下可以得到的现金数量。

数据范围
1≤T≤50,
1≤N≤105
输入样例：
2
3
1 8 2
4
10 7 6 14
输出样例：
8
24
样例解释
对于第一组样例，阿福选择第2家店铺行窃，获得的现金数量为8。

对于第二组样例，阿福选择第1和4家店铺行窃，获得的现金数量为10+14=24。
    
    
```

 



##### dfs暴力搜索

```c++
#include<iostream>
using namespace std;
int T,n;
const int N=110;
int arr[N];
int dfs(int x)
{
    if(x>n) return 0;
    else return max(dfs(x+1),dfs(x+2)+arr[x]);
}
int main()
{
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d",&n);
        for(int i=1;i<=n;i++) scanf("%d",arr[i]);
        int res=dfs(1);
        printf("%d\n",res);
    }
    return 0;

}
```



##### 记忆化搜索：（dfs的参数尽可能少，num的维数是dfs的参数个数）

```c++
#include<iostream>
using namespace std;
int T,n;
const int N=110;
int arr[N];
int num[N];//num[i]记录的是从第i家到第n家能偷的最大值
int dfs(int x)
{
    if(num[x]) return num[x];
    int sum=0;
    if(x>n) sum=0;
    else sum=max(dfs(x+1),dfs(x+2)+arr[x]);//不偷和偷
    num[x]=sum;
    return sum;
}
int main()
{
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d",&n);
        for(int i=1;i<=n;i++) scanf("%d",&arr[i]);
        int res=dfs(1);
        printf("%d\n",res);
    }
    return 0;

}
```



##### 动态规划：

n由大到小

```c++
#include<iostream>
using namespace std;
int T,n;
const int N=110;
int arr[N];
int f[N];

int main()
{
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d",&n);
        for(int i=1;i<=n;i++) scanf("%d",&arr[i]);
        memset(f,0,sizeof f);
        for(int i=n;i>=1;i--)//
            f[i]=max(f[i+1],f[i+2]+arr[i]);
        printf("%d\n",f[1]);
        
    }
    return 0;

}
```

n由小到大

```c++
#include<iostream>
using namespace std;
int T,n;
const int N=110;
int arr[N];
int f[N];

int main()
{
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d",&n);
        for(int i=1;i<=n;i++) scanf("%d",&arr[i]);
        memset(f,0,sizeof f);
        for(int i=1;i<=n;i++)
            f[i+2]=max(f[i+1],f[i]+arr[i]);
            //f[i]=max(f[i-1],f[i-2]+arr[i]);
        	//printf("%d\n",res)/
        printf("%d",f[n+2]);//舍弃f[1],f[2];避免越界
    }
    return 0;

}
```

##### 空间优化,不用f【N】数组：

```c++
#include<iostream>
using namespace std;
int T,n;
const int N=110;
int arr[N];


int main()
{
    scanf("%d",&T);
    while(T--)
    {
        scanf("%d",&n);
        for(int i=1;i<=n;i++) scanf("%d",&arr[i]);
        int newf=0,temp1=0,temp2=0;
        for(int i=1;i<=n;i++)
        {
            newf=max(temp1,temp2+home[i]);
              temp2=temp1;
            temp1=newf;//难想，自己悟吧
        }
    }
    return 0;

}
```

#### P1216 [IOI 1994 / USACO1.5] 数字三角形 Number Triangles(洛谷)

````c++
# P1216 [IOI 1994 / USACO1.5] 数字三角形 Number Triangles

## 题目描述

观察下面的数字金字塔。


写一个程序来查找从最高点到底部任意处结束的路径，使路径经过数字的和最大。每一步可以走到左下方的点也可以到达右下方的点。


在上面的样例中，从 $7 \to 3 \to 8 \to 7 \to 5$ 的路径产生了最大权值。

## 输入格式

第一个行一个正整数 $r$，表示行的数目。

后面每行为这个数字金字塔特定行包含的整数。

## 输出格式

单独的一行，包含那个可能得到的最大的和。

## 输入输出样例 #1

### 输入 #1

```
5
7
3 8
8 1 0
2 7 4 4
4 5 2 6 5
```

### 输出 #1

```
30
```

## 说明/提示

【数据范围】  
对于 $100\%$ 的数据，$1\le r\le 1000$，所有输入在 $[0,100]$ 范围内。

题目翻译来自 NOCOW。

IOI1994 Day1T1 / USACO Training Section 1.5。
````

##### 直接dfs(还是会超时)

```c++
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
int n;
const int N=1010;
int arr[1010][1010];
int dfs(int x,int y)
{
    if(x>n||y>n) return 0;
    return max(dfs(x+1,y),dfs(x+1,y+1))+arr[x][y];
}
int main()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        for(int j=1;j<=i;j++)
            scanf("%d",&arr[i][j]);
    int res=dfs(1,1);
    printf("%d",res);
    return 0;
}
```

##### 记忆化搜索(还是会超时一个)

```c++
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
int n;
const int N=1010;
int arr[1010][1010];
int mem[1010][1010];
int dfs(int x,int y)
{
    if(mem[x][y]) return mem[x][y];
    int sum=0;
    if(x>n||y>n) sum= 0;
    else sum=max(dfs(x+1,y),dfs(x+1,y+1))+arr[x][y];
    mem[x][y]=sum;
    return sum;
}
int main()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        for(int j=1;j<=i;j++)
            scanf("%d",&arr[i][j]);
    int res=dfs(1,1);
    printf("%d",res);
    return 0;
}
```

##### dp

```c
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
int n;
int arr[1010][1010];
int mem[1010][1010];
int main()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
        for(int j=1;j<=i;j++)
            scanf("%d",&arr[i][j]);
    for(int i=n;i>=1;i--)
        for(int j=i;j>=1;j--)//for(int j=1;j<=i;j++)
            mem[i][j]=max(mem[i+1][j],mem[i+1][j+1])+arr[i][j];
    printf("%d",mem[1][1]);
    return 0;
}
```

##### 二维变一维

```c
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
int n;
int arr[1010][1010];
int mem[1010];
int main()
{
    scanf("%d",&n);
    for(in
        t i=1;i<=n;i++)
        for(int j=1;j<=i;j++)
            scanf("%d",&arr[i][j]);
    for(int i=n;i>=1;i--)
        for(int j=1;j<=i;j++)
            mem[j]=max(mem[j],mem[j+1])+arr[i][j];
    printf("%d",mem[1]);
    return 0;
}
```

<img src="./c++学习笔记.assets/21af8e8627cfc4ec9d2b0aaf34eb3efa.jpeg" alt="21af8e8627cfc4ec9d2b0aaf34eb3efa" style="zoom: 25%;" />

#### 背包问题（acwing 2）

```c
有 N
 件物品和一个容量是 V
 的背包。每件物品只能使用一次。

第 i
 件物品的体积是 vi
，价值是 wi
。

求解将哪些物品装入背包，可使这些物品的总体积不超过背包容量，且总价值最大。
输出最大价值。

输入格式
第一行两个整数，N，V
，用空格隔开，分别表示物品数量和背包容积。

接下来有 N
 行，每行两个整数 vi,wi
，用空格隔开，分别表示第 i
 件物品的体积和价值。

输出格式
输出一个整数，表示最大价值。

数据范围
0<N,V≤1000

0<vi,wi≤1000

输入样例
4 5
1 2
2 4
3 4
4 5
输出样例：
8
```

解析：

##### dfs(必定超时)

```c
#include<iostream>
using namespace std;
int N,V;
int v[1010],W[1010];
int dfs(int x,int sur)
{
    if(x>N) return 0;
    if(sur<=0) return 0;
    if(sur<v[x]) return  dfs(x+1,sur);//这一步必不可少，
    return max(dfs(x+1,sur),dfs(x+1,sur-v[x])+W[x]);
}
int main()
{
    scanf("%d%d",&N,&V);
    for(int i=1;i<=N;i++)
        {
            scanf("%d%d",&v[i],&W[i]);
        }
    int res=dfs(1,V);
    printf("%d",res);
    return 0;
}
```

