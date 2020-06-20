# LeetCode刷题笔记



## 数组

### 1:两数之和

```js
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

```js
//双层for循环暴力破解法
var twoSum = function(nums, target) {
    let arr = [];
    for(let i = 0;i < nums.length;i++){
        for(let j = 0;j < nums.length;j++){
            if(nums[i]+nums[j] == target && i != j){
                arr.push(i,j);
                return arr
            }
        }
    }
};
```

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let temp = [];
    for(let i = 0;i <nums.length;i++){
        var dif = target-nums[i];
        if(temp[dif] != undefined){
            return [temp[dif],i]
        }
        temp[nums[i]] = i;
    }
};
```

通过下标的方式记录下当前遍历到的值，当后面数字与目标的差值等于之前遍历到的值则将其返回，其中当前遍历到的值每一轮都会记下轮数
也就是说将差值作为下标记录，value记录轮数