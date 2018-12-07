# 题目描述  
给出两个**非空**的链表用来表示两个非负的整数。其中，它们各自的位数是按照**逆序**的方式存储的，并且它们的每个节点只能存储**一位**数字。<br/>  
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。  
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。  
## 示例：  
```
输入：(2->4->3)+(5->6-> 4)
输出：7->0- 8
原因：342 + 465 = 807  
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
``` javascript
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
## 关于链表  
### 什么是链表  
要存储多个元素，数组可能是最常用的数据结构。这种数据结构非常方便，但是有一个缺点：从数组的起点或者中间插入或移除项的成本非常高，因为需要移动元素（比如你插入一个元素后面的所有的元素都移动了“位置”）。

链表存储有序的元素集合，但是不同于数组，链表中的元素在内存中并不是连续放置的。每个元素都是由一个存储元素本身的节点和一个指向下一元素的引用（也叫指针或者链接）组成。  

相比于数组来说，链表的好处在于添加或者删除元素的时候不需要移动其他元素。但是操作链表需要使用指针。数组的一个优点是可以直接访问任何位置的任何元素，但是要是想访问链表中的某一元素，则是必须从起点开始迭代直到找到目标元素。  
### 链表的学习  
创建一个链表  

``` javascript
function LinkedList() {
    var Node = function(element) {
        this.element = element;
        this.next = null;
    }

    //各种方法
}
```

Node表示要加入列表的项，它包含一个element属性以及一个next属性，element表示要添加到列表的值，next表示指向列表下一个节点项的指针。  
#### 当一个Node元素被创建时，它的next指针总是null  
<ul><li>向链表尾部追加元素</li></ul>  
列表为空，添加的是第一个元素。列表不为空，向其追加元素。  
#### 要循环访问列表中的所有元素，就需要有一个起点，就是head

``` javascript
this.append = function(element) {
    var node = new Node(element), //传入值创建Node项
        current;

    if(head === null) { //如果为空链表
        head = node; //设置node为head（head为第一个节点的引用）
    } else {
        current = head; //从表头开始
        while(current.next) { 
            //循环列表，找到最后一项（列表最后一个节点的下一个元素始终是null）
            current = current.next;
        }
        //使当前最后一项的指针指向node
        current.next = node;
    }
    length++; //更新列表长度
};
```
使用append  
``` javascript
var list = new LinkedList();
list.append(15);
list.append(10);
```  

<ul><li>从链表移除元素</li></ul>  
输入位置，从特定位置移除一个元素  

``` javascript
this.removeAt = function(position) {
    if(position > -1 && position < length) { //有效性检测
        var current = head, //用current来循环列表
        previous,
        index = 0;

        if(position === 0) {
            head = current.next; //移除第一个元素，直接把head指向下一个元素
        } else {
            while(index++ < position) { //循环列表找到满足条件的那个元素
                previous = current; //
                current = current.next; //把下一个变量覆给current
            }
            //跳过current，将当前要移除的元素的上一个与下一项直接连接起来。
            previous.next = current.next;
        }
        length --;
        return current.element;
    } else {
        return null;
    }
}
```  

在任意位置插入一个元素  

``` javascript
this.insert = function (position, element) {
    if(position >= 0 && position <= length) {
        var node = new Node(element),
            current = head; //通过current从head位置开始迭代
            previous,
            index = 0;

        if(position === 0) { //第一个位置
            node.next = current; //此时current = head,指向head那么node就成了第一个
            head = node; //node指向为head
        } else {
            while (index++ < position ) { //循环迭代到目标位置
                previous = current; 
                current = current.next;
            }

            node.next = current; // node的下一个为current
            previous.next = node; // node的上一个位置为previous
        }
        length++;
        return true;
    } else {
        return false;
    }
}
```  

把LinkedList对象转换成一个字符串。  

``` javascript
this.toString = function() {
    var current = head,
        string = '';
    while(current) { //循环访问列表
        string += current.element + (current.next ? '\n' : '');
        current = current.next;
    }
    return string; //返回字符串
}
```
返回元素的位置  

``` javascript
this.indexOf = function(element) {
    var current = head,
        index = 0;
    while(current) {
        if(element === current.element) {
            return index; //找到返回当前位置
        }
        index ++;
        current = current.next;
    }
    return -1;    //找不到返回-1
}  
```
