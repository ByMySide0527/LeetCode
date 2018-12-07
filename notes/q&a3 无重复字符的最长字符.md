# 题目描述  
给定一个字符串，请你找出其中不含有重复字符的**最长子串**的长度。
  
  
## 示例1：  
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```  
## 示例2：  
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```  
## 示例3：  
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```  
### 自己解题  
#### 暴力法    
```  
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    var a=[];
    var len=[];
    for(var i in s){
        if(a.includes(s.charAt(i))){
            len.push(a.length);
            var num=a.indexOf(s.charAt(i));
            a=a.slice(num+1);
            a.push(s.charAt(i));
        }else{
            a.push(s.charAt(i));
        }
    }
    len.push(a.length);
    return Math.max.apply(null,len)
}; 
```
## 心得  
<ul><li>Javascript中Math.max.apply和Math.max的区别</li></ul>  
Javascript中的Math.max方法可以求出给定参数中最大的数。  
```
> Math.max('1','2','3.1','3.2')
< 3.2
> Math.min(1,0,-1)
< -1 
```  
<br/>  
但如果是数组，就不能这样调用了。  
此时就用到了apply方法：  
```
apply 方法 (Function) (JavaScript)

调用函数，并用指定对象替换函数的 this 值，同时用指定数组替换函数的参数。

apply([thisObj[,argArray]])

thisObj
　　可选。 要用作 this 对象的对象。
argArray
　　可选。 要传递到函数的一组参数。  
```  
巧妙地使数组也可以调用Math.max和Math.min。  
```
> Math.max.apply(null, ['1','2','3.1','3.2'])
< 3.2
> Math.min.apply(null, [1,0,-1])
< -1
```  
#### apply()与call()的区别  
JavaScript中的每一个Function对象都有一个apply()方法和一个call()方法，它们的语法分别为：  
```
/*apply()方法*/
function.apply(thisObj[, argArray])

/*call()方法*/
function.call(thisObj[, arg1[, arg2[, [,...argN]]]]);  
```
<ul>
<li>它们各自的定义：</li>
apply：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即A对象应用B对象的方法。  
call：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.call(A, args1,args2);即A对象调用B对象的方法。
<li>它们的共同之处：</li>
都“可以用来代替另一个对象调用一个方法，将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象”。
<li>它们的不同之处：</li>
apply：最多只能有两个参数——新this对象和一个数组argArray。如果给该方法传递多个参数，则把参数都写进这个数组里面，当然，即使只有一个参数，也要写进数组里。如果argArray不是一个有效的数组或arguments对象，那么将导致一个TypeError。如果没有提供argArray和thisObj任何一个参数，那么Global对象将被用作thisObj，并且无法被传递任何参数。
call：它可以接受多个参数，第一个参数与apply一样，后面则是一串参数列表。这个方法主要用在js对象各方法相互调用的时候，使当前this实例指针保持一致，或者在特殊情况下需要改变this指针。如果没有提供thisObj参数，那么 Global 对象被用作thisObj。 
实际上，apply和call的功能是一样的，只是传入的参数列表形式不同。
</ul>
