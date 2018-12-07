# 题目描述  
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的**两个**整数。  

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。  
## 示例：  
```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```  
### 自己解题  
#### 暴力法  
暴力法很简单。遍历每个元素 *x* ，并查找是否存在一个值与 *target - x* 相等的目标元素。  
``` javascript  
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for(var i=0;i<nums.length;i++){
        for(var j=i+1;j<nums.length;j++){
            if(nums[j]==target-nums[i]){
                return [i,j];
            }
        }
    }
};  
```  
### 方法二（只用一遍循环，多一次判断，耗时少）  
``` javascript  
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let num1 = null;
    let num2 = null;
    for(let i=0;i<nums.length;i++){
        let item = target-nums[i];
        if(nums.includes(item)){
            if(nums.indexOf(item)!=i){
                num1 = i;
                num2 = nums.indexOf(item);
                break
            }
        }
    }
    return [num1,num2]

};  
```
