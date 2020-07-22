### 1.两数之和

#### 题目

```
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
```

#### 代码1

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for(let i = 0;i < nums.length;i++){
        for(let j = 0;j < nums.length;j++){
            if(nums[i]+nums[j] == target && i != j){
                let number = [];
                number.push(i);
                number.push(j);
                return number;
            }
        }
    }
};
/*
执行用时:184 ms
内存消耗:34.7 MB
思路:暴力破解法循环遍历数组，将数组的每一个值都取出来相加一次判断是否等于target
*/
```

#### 代码2

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let map = {};//key数字 value下标
    let loop = 0;//循环次数
    let dis;//目标与当前值的差
    while(loop < nums.length){
        dis = target - nums[loop];
        if(map[dis] != undefined){
            return [map[dis], loop];
        }
        map[nums[loop]] = loop;
        loop++;
    }
    return;
};
思路:
```

#### 代码3

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    var temp = [];
    for(var i=0;i<nums.length;i++){
        var dif = target - nums[i];
        if(temp[dif] != undefined){
            return [temp[dif],i];
        }
        temp[nums[i]] = i;
    }
};
思路:
```



### 2.整数反转

#### 题目

```
给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转
示例 1:
输入: 123
输出: 321
注意:
假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。
```

#### 代码1

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    //思路:转化为数组进行翻转，取消0
    if(x === 0){return 0;}
    let isPostive;
    if(x < 0){
        isPostive = true;
    }
    x = x+'';
    let arr = new Array();
    for(let i = 0;i<=x.length;i++){
        arr.push(x.charAt(i));
    }
    arr.reverse();
    if(arr[0] == 0){
        arr.shift();
    }
    x = parseInt(arr.toString().replace(/,/g,''));
    if(isPostive){
        x=-x;
    }
    if(x > Math.pow(2,31)-1 || x < Math.pow(-2,31)){
        return 0;
    }
    return x;
};
执行用时 :100 ms
内存消耗 :36.8 MB
```

#### 代码1简洁

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let now = Math.abs(x).toString().split("").reverse().join("");
    if(x < 0){
        return now <= Math.pow(2,31) ? -now : 0;
    }else{
        return now < Math.pow(2,31) ? now : 0;
    }
};
```

#### 代码2

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let ord = Math.abs(x);//去符号
    let now = 0;
    while(ord > 0){
        now = now * 10 + ord % 10;
        ord = Math.floor(ord / 10);
    }
    if(x < 0){
        return now <= Math.pow(2,31) ? -now : 0;
    }else{
        return now < Math.pow(2,31) ? now : 0;
    }
};
```





### 3.回文数

#### 题目

```
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:
输入: 121
输出: true
示例 2:
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

#### 代码1

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    return x.toString() === x.toString().split("").reverse().join("")
};
//思路:将数字转换成字符串，然后将字符串转化为以""分割的字符串数组，然后将数组反转，再将数组转为字符串相比较
```

#### 代码2

```javascript

```







### 罗马数字

#### 题目

```
罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：
I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。
```

#### 代码1

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
    let num = 0
    s.replace(/IV/g,'IIII')
    .replace(/IX/g,'IIIIIIIII')
    .replace(/XL/g,'XXXX')
    .replace(/XC/g,'XXXXXXXXX')
    .replace(/CD/g,'CCCC')
    .replace(/CM/g,'CCCCCCCCC')

    .split("").map(function(item,index,array){
        if(item == 'I'){
            num += 1;
        }else if(item == 'V'){
            num += 5;
        }else if(item == 'X'){
            num += 10;
        }else if(item == 'L'){
            num += 50;
        }else if(item == 'C'){
            num += 100;
        }else if(item == 'D'){
            num += 500;
        }else if(item == 'M'){
            num += 1000;
        }
       
    })
     return num;
};
```

#### 代码2

```javascript

```



