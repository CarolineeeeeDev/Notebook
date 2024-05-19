# 剑指offer

[TOC]

## 数组

### [数组中重复的数据 ](https://leetcode.cn/problems/find-all-duplicates-in-an-array/description/)

#### 将元素交换到对应的位置

```c++
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> result;
        for (int i = 0; i<nums.size();i++)
        {
            while (nums[i] != nums[nums[i]-1])
            {
                swap(nums[i],nums[nums[i]-1]);
            }
        }
        for (int i = 0; i<nums.size();i++)
        {
            if (nums[i]-1 != i)
            {
                result.push_back(nums[i]);
            }
        }
        return result;
    }
};
```

时间复杂度O(n)

空间复杂度O(1)

### 二维数组中的查找

#### 二叉搜索树

```c++
class Solution{
public:
    bool Find(int target, vector<vector><int> arr){
        if (arr.empty() || arr[0].empty()) return false;
        int i = 0;//行
        int j = arr.size()-1;//列
        while (i<=arr.size()-1 && j>=0)
        {
            if (target == arr[i][j])
                return true;
            else if (tartget < arr[i][j])
                --j;
            else
                ++i;
        }
        return false;
    }
}
```

类似于二叉搜索树：

<img src="images\1.png" alt="1" style="zoom: 50%;" />

### [旋转数组的最小数字](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba?tpId=13&tqId=11159&ru=/exam/oj)

#### 二分查找

最小值一定在右区域！

```c++
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param nums int整型vector 
     * @return int整型
     */
    int minNumberInRotateArray(vector<int>& nums) {
        int left = 0, right = nums.size()-1;
        int mid;
        while (left<right)
        {
            mid = (left + right)/2;
            if (nums[left]<nums[right])//left一定在左区域或最低点，right一定在右区域，左区域的数一定大于等于右区域的数
            return nums[left];
            if (nums[mid] > nums[right])//mid在左区域,最小的数字在mid右边
            {
                left = mid + 1;
            }
            else if (nums[mid] == nums[right])//mid在重复元素
            {
                --right;
            }
            else //mid在右区域, 最小数字要么是mid要么在mid左边
            {
                right = mid;
            }
            
        }
        return nums[left];
    }
};
```

### [数组中出现次数超过一半的数字](https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=13&tqId=11181&ru=/exam/oj)

#### 相互抵消

用不同数字相互抵消的方法，最后留下来的一定是超过一半的数字

```c++
    int MoreThanHalfNum_Solution(vector<int>& numbers) {
        // write code here
        int num = numbers[0];
        int count = 1;
        for (int i = 1; i<numbers.size(); ++i)
        {
            if (count > 0)
            {
                if (numbers[i]==num)
                {
                    ++count;
                }
                else 
                {
                    --count;
                }
            }
            else //count = 0
            {
                num = numbers[i];
                count = 1;
            }
        }
        return num;
    }
};
```

[1287. 有序数组中出现次数超过25%的元素 ](https://leetcode.cn/problems/element-appearing-more-than-25-in-sorted-array/description/)

由于这题是升序，可以直接用步长判断，也可以用上题的步骤判断

### [连续子数组的最大和(二)](https://www.nowcoder.com/practice/11662ff51a714bbd8de809a89c481e21?tpId=196&tqId=39301&ru=/exam/oj)

根据剑指offer自己想的，待优化：

> int最大值INT_MAX，最小值INT_MIN
>
> int的最小值可以写成0x8000000，最大值可以写成0x7FFFFFFF

```c++
class Solution {
public:
    vector<int> FindGreatestSumOfSubArray(vector<int>& arr) {
        // write code here
        int result = 0x80000000;
        vector<int> vresult;
        vector<int> temp;
        int sum = 0;
        for (int i =0;i<arr.size();++i)
        {
            if (sum<0)//如果和为负数，那么前一个和一定是从那个元素开始算的最大和了
            {
                temp.clear();
                temp.push_back(arr[i]);
                sum=arr[i];
            }
            else 
            {
                sum+=arr[i];
                temp.push_back(arr[i]);
            }
            if (sum>=result)
            {
                result = sum;
                vresult = temp;
            }
        }
        return vresult;
    }
};
```

#### 动态规划

```c++
//只需要保存最大值时：
int res = nums[0];
for (int i = 1; i < nums.size(); i++) {
    if (nums[i - 1] > 0) nums[i] += nums[i - 1];
    if (nums[i] > res) res = nums[i];
}
return res;
//需要保存对应的子数组时：

```

[求连续子数组的最大和](https://www.nowcoder.com/practice/8705437354604a7cb9ba7bf959e42de6?tpId=131&tqId=33839&ru=/exam/oj)（ACM模式）

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main() {
    string str;
    cin>>str;//输入是个字符串
    int k =0;
    vector<int> numbers;
    while((k = str.find(',')) != str.npos){//注意输出的方法
        string temp = str.substr(0, k);
        numbers.push_back(stoi(temp));
        str = str.substr(k + 1);
    }
    numbers.push_back(stoi(str));
    int tempmax = 0;
    int result = 0x80000000;
    int sum = 0;
    for (int i =0; i<numbers.size();++i)
    {
        if (sum<0)
        {
            sum=numbers[i];
        }
        else 
        {
            sum+=numbers[i];
        }
        result = max(sum,result);
    }
    if (result<0)
    {
        result = 0;
    }
    printf("%d",result);
}
// 64 位输出请用 printf("%lld")
```

## 链表

### [从尾到头打印链表](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035?tpId=13&tqId=11156&ru=/exam/oj)

#### 栈

利用栈先入后出的特点，很好解决

```c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        stack<int> stk;
        vector<int> result;
        int value = 0;
        while (head!=nullptr)
        {
            stk.push(head->val);
            head = head->next;
        }
        while (!stk.empty())
        {
            value = stk.top();
            result.push_back(value);
            stk.pop();
        }
        return result;
    }
};
```

时间复杂度O(n)

空间复杂度O(n)

#### 反转链表（双指针、递归）

双指针：

```c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        ListNode* preNode = nullptr;
        ListNode* curNode = head;
        
        while(curNode!=nullptr)
        {
            ListNode* temp = curNode->next;
            curNode->next = preNode;
            preNode = curNode;
            curNode = temp;
        }
        vector<int> result;
        while(preNode!=nullptr)
        {
            result.push_back(preNode->val);
            preNode = preNode->next;
        }
        return result;
    }
};
```

时间复杂度O(n)

空间复杂度O(1)

==递归==：

```c++
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        ListNode* newhead = ReverseList(head);
        vector<int> result;
        while (newhead!=nullptr)
        {
            result.push_back(newhead->val);
            newhead = newhead->next;
        }
        return result;
    }

    ListNode* ReverseList(ListNode* head)
    {
        if (head==nullptr || head->next==nullptr)
        {
            return head;
        }
        ListNode* newhead = ReverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return newhead;
    }
};
```

时间复杂度O(n)

空间复杂度O(n)

#### 拓展：反转链表中间一部分

[92. 反转链表 II - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-linked-list-ii/description/)

```c++
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (head->next==nullptr || left==right)
        {
            return head;
        }
        ListNode* dummyhead = new ListNode(0);
        dummyhead->next = head;
        ListNode* preleftEdge = dummyhead;
        ListNode* leftEdge = head;
        ListNode* rightEdge = head;
        for(int i = 1; i<left;++i)
        {
            preleftEdge = preleftEdge->next;
            leftEdge = preleftEdge->next;
        }
        for(int i = 1; i<right;++i)
        {
            rightEdge = rightEdge->next;
        }
        ListNode* nextrightEdge = rightEdge->next;
        
        ListNode* leftNode = leftEdge;
        ListNode* firstNode = leftNode;
        ListNode* rightNode = leftNode->next;
        while (rightNode!=nextrightEdge)
        {
            ListNode* temp = rightNode->next;
            rightNode->next = leftNode;
            leftNode = rightNode;
            rightNode = temp;
        }
        preleftEdge->next = leftNode;
        firstNode->next = nextrightEdge;
        return dummyhead->next;
    }
};
```



### [删除链表的节点](https://www.nowcoder.com/practice/f9f78ca89ad643c99701a7142bd59f5d?tpId=265&tqId=39280&ru=/exam/oj)

```c++
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param head ListNode类 
     * @param val int整型 
     * @return ListNode类
     */
    ListNode* deleteNode(ListNode* head, int val) {
        // write code here
        ListNode* dummyhead = new ListNode(0);
        dummyhead->next = head;
        ListNode* pre = dummyhead;
        ListNode* cur = head;
        while (cur!=nullptr)
        {
            if (cur->val==val)
            {
                pre->next = cur->next;
                break;
            }
            else 
            {
                cur = cur->next;
                pre = pre->next;
            }
        }
        return dummyhead->next;
    }
};
```

还有一种不需要知道前驱结点就可以“删除”链表结点的方法,前提是不能删除最后一个结点：

```c++
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```



### [链表合并](https://www.nowcoder.com/practice/46bda7f0570a47b6b54a29a0a6ae4c27?tpId=182&tqId=34634&ru=/exam/oj)

ACM模式的话要注意输入输出，然后要注意cur指针的更新

```c++
#include <iostream>
using namespace std;
struct ListNode
{
    int val;
    ListNode* next;
    ListNode(int val): val(val), next(nullptr){}
};

int main() {
    int a;
    ListNode* dummyhead = new ListNode(0);
    ListNode* cur = dummyhead;
    ListNode* dummyhead1 = new ListNode(0);
    ListNode* cur1 = dummyhead1;
    ListNode* dummyhead2 = new ListNode(0);
    ListNode* cur2 = dummyhead2;
    while(cin>>a)
    {
        ListNode* node = new ListNode(a);
        cur1->next = node;
        cur1 = cur1->next;
        if(cin.get()=='\n')
        {
        break;
        }
    }
    while(cin>>a)
    {
        ListNode* node = new ListNode(a);
        cur2->next = node;
        cur2 = cur2->next;
    }
    cur1 = dummyhead1->next;
    cur2 = dummyhead2->next;
    while (cur1!=nullptr && cur2!=nullptr)
    {
        if (cur1->val<=cur2->val)
        {
            cur->next = cur1;
            cur1 = cur1->next;
        }
        else 
        {
            cur->next = cur2;
            cur2 = cur2->next;
        }
        cur = cur->next;
    }
    if (cur1==nullptr)
    {
        cur->next = cur2;
    }
    if (cur2==nullptr)
    {
        cur->next = cur1;
    }
    
    cur = dummyhead->next;
    
    while (cur!=nullptr)
    {
        printf("%d ",cur->val);
        cur = cur->next;
    }
    return 0;
}
// 64 位输出请用 printf("%lld")
```

### [链表中倒数最后k个结点](https://www.nowcoder.com/practice/886370fe658f41b498d40fb34ae76ff9?tpId=13&tqId=1377477&ru=/exam/oj/ta&qru=/ta/coding-interviews/question-ranking&sourceUrl=%2Fexam%2Foj%2Fta%3Fpage%3D1%26tpId%3D13%26type%3D13)

#### 双指针思想

右指针指向左指针后k个元素，这样当右指针为最后一个节点后的元素时，左指针指向的就是所求元素

```c++
/**
 * struct ListNode {
 *	int val;
 *	struct ListNode *next;
 *	ListNode(int x) : val(x), next(nullptr) {}
 * };
 */
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param pHead ListNode类 
     * @param k int整型 
     * @return ListNode类
     */
    ListNode* FindKthToTail(ListNode* pHead, int k) {
        // write code here
        if (pHead==nullptr)
        {
            return nullptr;
        }
        ListNode* left = pHead;
        ListNode* right = left;
        for (int i =0; i<k;++i)
        {
            if(right==nullptr)
            {
                return nullptr;
            }
            right = right->next;  
        }
        while (right!=nullptr)
        {
            right = right->next;
            left = left->next;
        }
        return left;
    }
};
```

### [复杂链表的复制](https://www.nowcoder.com/practice/f836b2c43afc4b35ad6adc41ec941dba?tpId=13&tqId=23254&ru=%2Fpractice%2F886370fe658f41b498d40fb34ae76ff9&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&sourceUrl=)

[LCR 154. 复杂链表的复制 - 力扣（LeetCode）](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/description/)

#### 哈希表

键为旧指针，值为新指针。第一次遍历时初始化键和值的label，第二次赋上next和random指针

```c++
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (head==nullptr)
        {
            return nullptr;
        }

        unordered_map<Node*,Node*> mp;

        Node* cur = head;
        while (cur!=nullptr)
        {
            Node* newNode = new Node(cur->val);
            mp[cur] = newNode;
            cur = cur->next;
        }
        cur = head;
        while (cur!=nullptr)
        {
            mp[cur]->next = mp[cur->next];
            mp[cur]->random = mp[cur->random];
            cur = cur->next;
        }
        return mp[head];

    }
};
```

#### 在每个旧节点后加上新节点

最后要记得把旧链表头结点断开连接

```c++
class Solution {
public:
    RandomListNode* Clone(RandomListNode* pHead) {
        if (pHead==nullptr)
        {
            return nullptr;
        }
		//初始化next
        RandomListNode* cur1 = pHead;
        while (cur1!=nullptr)
        {
            RandomListNode* newNode = new RandomListNode(cur1->label);
            newNode->next = cur1->next;
            cur1->next = newNode;
            cur1 = cur1->next->next;
        }
		//赋值random
        cur1 = pHead;
        RandomListNode* cur2 = pHead->next;
        while (cur1!=nullptr)
        {
            if (cur1->random != nullptr)
            {
                cur2->random = cur1->random->next;
            }
            cur1 = cur1->next->next;
            cur2 = cur2->next->next;
        }
		//拆分链表
        RandomListNode* newCloneHead = pHead->next;
        cur2 = newCloneHead;
        pHead->next = nullptr;
        while (cur2->next!=nullptr)
        {
            cur2->next = cur2->next->next;
            cur2 = cur2->next;
        }
        cur2->next=nullptr;
        cur1 = pHead;
        cur2 = pHead->next;

        return newCloneHead;
    }
};
```

### [删除有序链表中重复的元素-I](https://www.nowcoder.com/practice/c087914fae584da886a0091e877f2c79?tpId=196&tqId=37064&ru=/exam/oj)

#### 双指针思想

```c++
    ListNode* deleteDuplicates(ListNode* head) {
        // write code here
        if (head==nullptr)
        {
            return nullptr;
        }
        ListNode* dummyhead = new ListNode(0);
        ListNode* left = dummyhead;
        ListNode* right = head;
        while(right!=nullptr)
        {
            while (right->next!=nullptr && right->val==right->next->val)
            {
                right = right->next;
            }
            left->next = right;
            left = left->next;
            right = right->next;
        }
        return dummyhead->next;
    }
```

### [删除链表中重复的结点](https://www.nowcoder.com/practice/fc533c45b73a41b0b44ccba763f866ef?tpId=13&tqId=11209&ru=/exam/oj)

比前面多了再将right右移一步的动作，以及最后要把left指向nullptr

```c++
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead) {
        if (pHead==nullptr)
        {
            return nullptr;
        }
        ListNode* dummyhead = new ListNode(0);
        ListNode* left = dummyhead;
        ListNode* right = pHead;
        while(right!=nullptr)
        {
            if(right->next!=nullptr && right->val==right->next->val)
            {
                while (right->next!=nullptr && right->val==right->next->val)
                {
                right = right->next;
                }
                right = right->next;
                continue;
            }
            left->next = right;
            left = left->next;
            right = right->next;
        }
        left->next = nullptr;
        return dummyhead->next;
    }
};
```

## 二叉树

### [二叉树的深度](https://www.nowcoder.com/practice/435fb86331474282a3499955f0a41e8b?tpId=13&tqId=11191&ru=/exam/oj)

#### 递归

返回左子树和右子树深度的最大值加上一（后序遍历）

```c++
class Solution {
public:
    int TreeDepth(TreeNode* pRoot) {
		if (pRoot==nullptr)
		{
			return 0;
		}
		return max(TreeDepth(pRoot->left),TreeDepth(pRoot->right))+1;
		
    }
};
```

### [二叉树的最小深度](https://www.nowcoder.com/practice/6a7f40d7696d46f79c74c61179993be6?tpId=196&tqId=39468&ru=/exam/oj)

[111. 二叉树的最小深度 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)

和二叉树的（最大）深度的区别是，计算的是到叶子节点（左右孩子都为空）的最小深度，也用后序遍历实现

```c++
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (root==nullptr)
        {
            return 0;
        }
        if (root->left==nullptr && root->right!=nullptr)
        {
            return minDepth(root->right)+1;
        }
        else if (root->right==nullptr && root->left!=nullptr)
        {
            return minDepth(root->left)+1;
        }
        else
        {
            return min(minDepth(root->left),minDepth(root->right))+1;
        }
    }
};
```

### [二叉树的镜像](https://www.nowcoder.com/practice/a9d0ecbacef9410ca97463e4a5c83be7?tpId=13&tqId=11171&ru=/exam/oj)

[LCR 144. 翻转二叉树 - 力扣（LeetCode）](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/description/)

前序遍历

```c++
TreeNode* Mirror(TreeNode* pRoot) {
        // write code here
        if (pRoot==nullptr) return pRoot;
        swap(pRoot->left,pRoot->right);
        Mirror(pRoot->left);
        Mirror(pRoot->right);
        return pRoot;
    }
```

后序遍历

```c++
TreeNode* Mirror(TreeNode* pRoot) {
        // write code here
        if (pRoot==nullptr) return pRoot;
        Mirror(pRoot->left);
        Mirror(pRoot->right);
        swap(pRoot->left,pRoot->right);
        return pRoot;
    }
```



## 队列、栈

### [用两个栈实现队列](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=13&tqId=23281&ru=/exam/oj/ta&qru=/ta/coding-interviews/question-ranking&sourceUrl=%2Fexam%2Foj%2Fta%3Fpage%3D1%26tpId%3D13%26type%3D13)

每当要pop的时候就获取stack2的最上面的元素，如果stack2为空，则将stack1依次出栈到stack2。这样stack2上面的就是最先push进去的元素，最底下是最新push进去的元素。

```c++
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        while (!stack2.empty())
        {
            int result = stack2.top();
            stack2.pop();
            return result;
        }
        while (!stack1.empty())
        {
            int temp = stack1.top();
            stack2.push(temp);
            stack1.pop();
        }
        int result = stack2.top();
        stack2.pop();
        return result;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```



## 动态规划

## 跳台阶

#### DP(ACM模式)

```c++
#include <iostream>
#include <unordered_map>

using namespace std;

int main() {
    int a;
    cin>>a;
    unordered_map<int,int> dp;
    dp[0] = 1;
    dp[1] = 1;
    dp[2] = 2;
    if (a<=2)
    {
        printf("%d",dp[a]);
    }
    else {
    for (int i=3;i<=a;i++)
    {
        int temp = dp[2];
        dp[2] +=dp[1];
        dp[1] = temp;
    }
    printf("%d",dp[2]);
    }
    
    return 0;
}
// 64 位输出请用 printf("%lld")

```

#### 递归(ACM模式)

```c++
#include <iostream>
using namespace std;
 
int Jump(int num)
{
    if (num==0) return 1;
    if (num==1) return 1;
    if (num==2) return 2;
    return Jump(num-1) + Jump(num-2);
}
 
int main() {
    int a;
    cin>>a;
    int result = Jump(a);
    printf("%d",result);
    return 0;
}
// 64 位输出请用 printf("%lld")

```

