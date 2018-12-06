# 题目描述  
给出两个**非空**的链表用来表示两个非负的整数。其中，它们各自的位数是按照**逆序**的方式存储的，并且它们的每个节点只能存储**一位**数字。<br/>  
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。  
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。  
## 示例：  
```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出： 7 -> 0 -> 8
原因： 342 + 465 = 807  
```   
### 解题思路：  
就像你在纸上计算两个数字的和那样，我们首先从最低有效位也就是列表 l1 和 l2的表头开始相加。由于每位数字都应当处于0…9的范围内，我们计算两个数字的和时可能会出现**“溢出”**。例如，5 + 7 = 12。在这种情况下，我们会将当前位的数值设置为 22，并将进位 carry = 1带入下一次迭代。进位 carrycarry 必定是 0 或 1，这是因为两个数字相加（考虑到进位）可能出现的最大和为 9 + 9 + 1 = 19。  
#### 需要注意的地方：  
|测试用例|示例说明|
|:---|:---|
|l1=[0,1]<br/>l2=[0,1,2]|当一个列表比另一个列表长时|
|l1=[]<br/>l2=[0,1]|当一个列表为空时，即出现空列表。|
|l1=[9,9]<br/>l2=[1]|求和运算最后可能出现额外的进位，这一点很容易被遗忘| 
<br/>  
  
## 伪代码  
<ul>
<li>将当前结点初始化为返回列表的哑结点。</li>
<li>将进位 carry初始化为 0。</li>
<li>将p和q分别初始化为列表l1和l2的头部。</li>
<li>遍历列表l1和l2直至到达它们的尾端
  <ul>
    <li>将x设为结点p的值。如果p已经到达l1的末尾，则将其值设置为0。</li>
    <li>将y设为结点q的值。如果q已经到达l2的末尾，则将其值设置为0</li>
    <li>设定 sum = x + y + carry。</li>
    <li>更新进位的值，carry = sum/10。</li>
    <li>创建一个数值为(sum mod 10) 的新结点，并将其设置为当前结点的下一个结点，然后将当前结点前进到下一个结点。</li>
    <li>同时，将p和q前进到下一个结点</li>
  </ul>
 </li>
<li>检查 carry = 1是否成立，如果成立，则向返回列表追加一个含有数字1新结点</li>
<li>返回哑节点的下一节点</li>
</ul>  

## 自己解题：  
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var p=l1;
    var q=l2;
    var num=0;
    var l3 = new ListNode(0);
    var l4=l3;
    while(p||q){
        var a = p?p.val:0;
        var b = q?q.val:0;
        l4.next=new ListNode((a+b+num)%10);
        num = parseInt((a+b+num)/10);
        if(p) p=p.next;
        if(q) q=q.next;
        l4=l4.next;
    }
    if(num)
        l4.next=new ListNode(num);
    return l3.next;
};
```
