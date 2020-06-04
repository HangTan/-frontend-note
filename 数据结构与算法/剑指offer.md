 

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



# 2、链表

链表应该是面试时被提及最频繁的数据结构。

![image-20200603072109421](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603072109421.png)

```js
// 链表的定义
function ListNode(val) {
    this.val = val;
    this.next = null;
}
```



## 面试题6：从尾到头打印链表

![image-20200603072614609](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603072614609.png)

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var reversePrint = function(head) {
  let stack = [];
  if (head === null) {
    return [];
  }
  while(head!==null) {
    stack.push(head.val);
    head = head.next;
  }
  return stack.reverse();
};
```



# 3、树

父节点和子节点之间用指针链接。

二叉树：前序、后续、中序遍历

<img src="C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603074658548.png" alt="image-20200603074658548" style="zoom:67%;" />

前序：10  6   4  8   14   12   16

后序：4  8  6  12   16  14  10

中序：4   8   6   12   16   14   10

![image-20200603074958857](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603074958857.png)

二叉搜索树，左子节点总是小于等于根节点，右子节点总是大于或等于根节点。平均在 **O(logn)** 的时间内根据数值在二叉搜索树中找到一个节点。

![image-20200603075251598](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603075251598.png)



## 面试题7：重建二叉树

![image-20200603075313332](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603075313332.png)

递归：

![image-20200603081218393](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200603081218393.png)

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */

function TreeNode(val) {
  this.val = val;
  this.left = this.right = null;
}

var buildTree = function (preorder, inorder) {
  let preLen = preorder.length;
  let inLen = inorder.length;

  if (preLen !== inLen) {
    return new Error();
  }

  let map = new Map();
  for (let i = 0; i < inLen; i++) {
    map.set(inorder[i], i);
  }

  return abuildTree(preorder, 0, preLen - 1, map, 0, inLen - 1);
};

function abuildTree(preorder, preLeft, preRight, map, inLeft, inRight) {
  if (preLeft > preRight || inLeft > inRight) {
    return null;
  }
  let rootVal = preorder[preLeft];
  let root = new TreeNode(rootVal);
  let pIndex = map.get(rootVal);
  root.left = abuildTree(
    preorder,
    preLeft + 1,
    pIndex - inLeft + preLeft,
    map,
    inLeft,
    pIndex - 1
  );
  root.right = abuildTree(
    preorder,
    pIndex - inLeft + preLeft + 1,
    preRight,
    map,
    pIndex + 1,
    inRight
  );
  return root;
}
```



## 面试题8：二叉树的下一个节点

![image-20200604072950199](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200604072950199.png)



# 4、栈和队列

![image-20200604074109956](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200604074109956.png)

![image-20200604074205146](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200604074205146.png)



## 面试题9：用两个栈实现队列

![image-20200604074310254](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200604074310254.png)

![image-20200604074750710](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200604074750710.png)

```js
var CQueue = function () {
  this.stack1 = [];
  this.stack2 = [];
};

/**
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function (value) {
  this.stack1.push(value);
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function () {
  if (this.stack2.length !== 0) {
    return this.stack2.pop();
  }
  if (!this.stack1.length) {
    return -1;
  }
  while (this.stack1.length) {
    this.stack2.push(this.stack1.pop());
  }
  return this.stack2.pop();
};

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */
```

相关题目：用两个队列实现一个栈。































































































