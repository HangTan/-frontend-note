 

# 1、数组

​		数组占据一块连续的内存并按照顺序存储数据。数组在内存中是连续的，可以根据下标在 O(1) 时间读/写任何元素，时间效率很高。也可以用数组来实现简单的哈希表：数组的下标设为哈希表的键值，数组中的每一个数字设为哈希表的值。

## 面试题 3：数组中重复的数字

![image-20200528075318295](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200528075318295.png)

### 解法一：先数组排序，从头到尾扫描。O(nlogn)

### 解法二：哈希表

​	    从头到尾顺序扫描数组的每个数字，每扫描到一个数字的时候，都可以用 O(1)的时间来判断哈希表里是否已经包含了该数字。时间复杂度 O(n)，空间O(n)。

改进：

![image-20200528080337376](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200528080337376.png)

![image-20200528080410889](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200528080410889.png)

时间复杂度 O(n)，所有操作都是在原数组上进行的，空间复杂度O(1)

```js
var findRepeatNumber = function(nums) {
  let hashMap = new Map();
  for(let i = 0; i < nums.length; i++) {
    if(hashMap.has(nums[i])) {
      return nums[i];
    }
    hashMap.set(nums[i], i);
    console.log(hashMap);
  }
};

var findRepeatNumber = function(nums) {
    nums.sort((a,b) => a - b);
    for(let i = 0; i< nums.length-1; i++) {
        if(nums[i] !== nums[i+1]){
            continue;
        }
        return nums[i];
    }
};
```



## 面试题4：二维数组中的查找

![image-20200529075653429](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200529075653429.png)

![image-20200529075749238](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200529075749238.png)

```js
// 从左下角开始查找
var findNumberIn2DArray = function(matrix, target) {
  let n = matrix.length - 1;
  let m = 0;
  while(n>=0 && m <= matrix[0].length) {
    if(target === matrix[n][m]) {
      return true;
    } else if (target > matrix[n][m]) {
      m += 1;
    } else {
      n -= 1;
    }
  }
  return false;
};
```



## 面试题5：替换空格

![image-20200531083931830](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200531083931830.png)

O(n)复杂度的算法：先遍历一遍字符串，查看有多少个空格m，然后新建一个数组扩容到原数组+2*m

然后用两个指针，P1指向原始字符串的末尾，P2指向新数组的末尾，从后往前开始遍历，非空格直接复制，遇到空格就替换，注意P1和P2遇到空格后移动的距离。

### 解法一：正则表达式

```
var replaceSpace = function(s) {
  return s.replace(/ /g, "%20");
};
```

### 解法二：双指针

```js
if (!s || !s.length) {
    return "";
  }
  let emptyNum = 0;
  let charNum = 0;
  for (let i = 0; i < s.length; i++) {
    if (s[i] === " ") {
      emptyNum++;
    } else {
      charNum++;
    }
  }

  const newLength = emptyNum * 2 + charNum;
  let newArray = new Array(newLength);
  for(let i = 0, j = 0; j < s.length; j++) {
    if(s[j] === ' ') {
      newArray[i++] = "%";
      newArray[i++] = "2";
      newArray[i++] = "0";
    } else {
      newArray[i++] = s[j];
    }
  }
  return newArray.join('');
```

### 举一反三：

![image-20200531094717765](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200531094717765.png)

在合并两个数组（包括字符串）时，如果从前往后复制每个数字（字符）则需要重复移动数字（或字符）多次，那么我们可以考虑从后往前复制，这样就能减少移动的次数，从而提高效率。























































































































































