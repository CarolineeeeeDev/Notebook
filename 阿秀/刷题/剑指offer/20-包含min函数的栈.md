# 包含min函数的栈

[TOC]

[包含min函数的栈_牛客题霸_牛客网 (nowcoder.com)](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49?tpId=13&&tqId=11173&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

[155. 最小栈 - 力扣（LeetCode）](https://leetcode.cn/problems/min-stack/description/)

[LCR 147. 最小栈 - 力扣（LeetCode）](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

[面试题 03.05. 栈排序 - 力扣（LeetCode）](https://leetcode.cn/problems/sort-of-stacks-lcci/description/)



## 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））



## 解法

### 只用一个栈

```c++
class Solution {
    int minNum = INT_MAX;
    stack<int> st;
public:
    void push(int value) {
        minNum = std::min(value, minNum);注意当前类中也有一个min函数，
        st.push(minNum);
        st.push(value);
        
    }
    void pop() {
        st.pop();//pop掉当前值
        st.pop();//pop掉当前最小值
        if(!st.empty()){
            int temp = st.top();
            st.pop();
            minNum = st.top();
            st.push(temp);
        }
        else
        {
            minNum = INT_MAX;
        }
       
    }
    int top() {
        return st.top();
    }
    int min() {
        return minNum;
    }
};
```

