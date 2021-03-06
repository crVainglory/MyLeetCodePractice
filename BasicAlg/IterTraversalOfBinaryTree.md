**二叉树的各种遍历：**

递归的方法都很简单， 这里只记录一些迭代的写法：



先说一个前序和后序都很方便使用的模板：
注意根左右的顺序
保证下一个要访问的元素永远在栈顶
因此算法流程就是：
访问当前， 保存之后要访问的左右子节点的信息
其中由于要先访问左节点 而用来保存的数据结构是栈，因此要先入右子节点

```c++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        if(!root) return {};
        vector<int> res;
        stack<TreeNode*> s;
        s.push(root);
        while(!s.empty()){
            auto tmp = s.top(); s.pop();
            res.push_back(tmp->val);
            if(tmp->right) s.push(tmp->right);
            if(tmp->left) s.push(tmp->left);
        }
        return res;
    }
};
```

此时后序遍历只是先序遍历的一个变种， 因为先序是根左右， 后序是左右根

因此我们只需要调整一下左右子节点入栈的顺序， 然后最后把数组翻转一下即可

这里翻转的写法是直接插入在数组的头部

```c++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        if(!root) return {};
        vector<int> res;
        stack<TreeNode*> s;
        s.push(root);
        while(!s.empty()){
            auto tmp = s.top(); s.pop();
            res.insert(res.begin(), tmp->val);
            if(tmp->left) s.push(tmp->left);
            if(tmp->right) s.push(tmp->right);
        }
        return res;
    }
};
```

