# 题目描述  
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 `"LEETCODEISHIRING"` 行数为 3 时，排列如下： 

```
L   C   I   R
E T O E S I I G
E   D   H   N
```

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"LCIRETOESIIGEDHN"`。

请你实现这个将字符串进行指定行数变换的函数：

```js
string convert(string s, int numRows);
```




## 示例1：  
``` 
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN" 
```
## 示例2：  
```
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释: 
L     D     R
E   O E   I I
E C   I H   N
T     S     G
```


### 自己解题  
#### 暴力法    
``` javascript 
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    var arr = [];
    for(var k = 0;k < numRows;k++){
        arr.push('');
    }//初始化
    var result = '';
    
    if(numRows > 1)
        var len = 2 * numRows - 2;
    else
        var len = 1;
    
    for(var i = 0;i<s.length;i++){
        var j = i % len;
        if(j >= numRows)
            j = 2 * numRows - j - 2;
        arr[j] = arr[j] + s[i];
    }
    for(k = 0;k < numRows;k++){
        result = result + arr[k];
    }
    return result
};
```
  



