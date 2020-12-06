# 题目

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

示例 1：

> 输入：
> ["CQueue","appendTail","deleteHead","deleteHead"]
> [[],[3],[],[]]
> 输出：[null,null,3,-1]

示例 2：

> 输入：
> ["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
> [[],[],[5],[2],[],[]]
> 输出：[null,-1,null,null,5,2]

# 标签

栈；队列

# 解题思路

意思是把第一个栈维护成 “被实现的队列”。对于每一个新加的元素，先把第一个栈的所有元素转移到第二个栈，然后把新加入的元素放到第一个栈中，最后把第二个栈的全部元素转移到第一个栈上。这样下来，新加进来的元素在第一个栈的最底部，所以就相当于后入后出。当删除队列头元素的时候，就只需要把第一个栈弹出一个元素即可，先入先出。如此，队列就被实现了。

# 代码

```java
class CQueue {
    Stack<Integer> stack1;
    Stack<Integer> stack2;
    int size; //代表队列元素个数

    public CQueue() {
        stack1=new Stack<>();
        stack2=new Stack<>();
        size=0;
    }
    
    public void appendTail(int value) {
        while(!stack1.empty()){
            //把stack1的元素暂放stack2中
            stack2.push(stack1.pop());
        }
        //向栈底压入新增元素
        stack1.push(value);
    
        //把stack2中的元素压入stack1中
        while(!stack2.empty()){
            stack1.push(stack2.pop());
        }
        size++;
    }
    
    public int deleteHead() {
        if(size==0)return -1;
        size--;
        return stack1.pop();
    }

}
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof

