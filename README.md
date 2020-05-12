# leetcode record for Huiming and NaNa

## <a name="Catalogue"/>Catalogue
I love nana
* Easy
    * [1. Two Sum](#1)
    * [2. 整数反转](#2)
    * [1365. how-many-numbers-are-smaller-than-the-current-number](#1365)
    * [4.  Linked List Cycle](#4)
    * [771.  jewels-and-stones](#771)


## <a name="1"> 1.Two Sum
-------------------------
### Question:
>Given an array of integers, return indices of the two numbers such that they add up to a >specific target.You may assume that each input would have exactly one solution, and you may >not use the same element twice.

### Example:

```
        Given nums = [2, 7, 11, 15], target = 9,
        Because nums[0] + nums[1] = 2 + 7 = 9,
        return [0, 1].
```

### Thinking
> put all numbers into a dictionary. if target - element in list  = another element in list 
>We use a dictionary to record the index of the list. the first element must be in the >dictionary because of the final list is consist by two numbers.

### Solution:

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        for i in range(len(nums)):
            if target - nums[i] in dic:
                return [dic[target-nums[i]],i]
            dic[nums[i]] = i
```

[back to Catalogue](#Catalogue)

-------------------------

    

## <a name="1"> 2. 整数反转
-------------------------
### Question:
>给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

### Example:

```
        示例 1:

输入: 123
输出: 321
 示例 2:

输入: -123
输出: -321
示例 3:

输入: 120
输出: 21
```

### 注意：
> 假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。
### Solution:

```python
class Solution:
    def reverse_force(self, x: int) -> int:
        if -10 < x < 10:
            return x
        str_x = str(x)
        if str_x[0] != "-":
            str_x = str_x[::-1]
            x = int(str_x)
        else:
            str_x = str_x[:0:-1]
            x = int(str_x)
            x = -x
        return x if -2147483648 < x < 2147483647 else 0

        def reverse_better(
        self, 
        x: int) -> int:
       
        
        y, res = abs(x), 0
        # 则其数值范围为 [−2^31,  2^31 − 1]
        boundry = (1<<31) -1 if x>0 else 1<<31
        while y != 0:
            res = res*10 +y%10
            if res > boundry :
                return 0
            y //=10
        return res if x >0 else -res



```

[back to Catalogue](#Catalogue)

-------------------------


## <a name="1365"> 1365. how-many-numbers-are-smaller-than-the-current-number
-------------------------
### Question:
>Given the array nums, for each nums[i] find out how many numbers in the array are smaller than it. That is, for each nums[i] you have to count the number of valid j's such that j != i and nums[j] < nums[i].

Return the answer in an array.

### Example:

```
       Input: nums = [8,1,2,2,3]
        Output: [4,0,1,1,3]
        Explanation: 
        For nums[0]=8 there exist four smaller numbers than it (1, 2, 2 and 3). 
        For nums[1]=1 does not exist any smaller number than it.
        For nums[2]=2 there exist one smaller number than it (1). 
        For nums[3]=2 there exist one smaller number than it (1). 
        For nums[4]=3 there exist three smaller numbers than it (1, 2 and 2).
```

### Thinking
> two for loop
### Solution:

```python
class Solution:
    def smallerNumbersThanCurrent(self, nums: List[int]) -> List[int]:
        result = []
        for value in nums:
            num = len([i for i in nums if i < value ])           
            result.append(num)
        return result
```

[back to Catalogue](#Catalogue)

## <a name="4"> 4. Linked List Cycle
### Question:
>给定一个链表，判断链表中是否有环。

>为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。



### Example:

       示例 1：

输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。

示例 2：

输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。

示例 3：

输入：head = [1], pos = -1
输出：false
解释：链表中没有环。


### Solution:

```python
法一：借助辅助空间

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        a = set() 
        while head:
            
            if head in a:
                return True

            a.add(head)
            head = head.next
        return False
```

>理解： 用一个set数据结构存储每个节点地址;
时间复杂度O(n*1)：访问每个节点O(n)+存储每个节点O(1);
空间复杂度O(n)

法二： 快慢指针法
``` c++
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        slow = fast = head
        # if not head：  # 没必要这样写可以加入while循环判断更简洁
        #     return False

        while fast and fast.next:  # 防止head为空和出现空指针的next的情况
            slow = slow.next
            fast = fast.next.next
            if slow is fast:
                return True

        return False
```

>理解：
思路：定义一个快指针和慢指针,每次快指针走2步，慢指针走1步，判断快指针是否与慢指针重逢
时间复杂度O(n+k)：
情况一：链表部分成环O(n)；
部分成环时，快指针先于慢指针进入环，慢指针进环时间O(n)；当快慢指针都进入环，假设环节点数量为K,当快慢指针第一次相遇时，快指针至少已经在环内已经比慢指针多走一圈(多走的这一圈是当慢指针进入后开始算的)，时间O(k)； 综上，时间复杂度O(k+n)，即为O(n)

>情况二：链表完全成环O(n)
        同起点，第一次相遇时，快指针已经在环内已经比慢指针多走一圈；时间复杂度O(n)

法三：递归标记法
``` c++
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head:
            return False

        if head == 0xcafebabe:
            return True

        head.val = 0xcafebabe
        return self.hasCycle(head.next)

)


```

>理解：
思路：把访问过的值都进行赋值，如果链表完全成环，则必会出现重复值
时间复杂度：O(n);访问O(n)+赋值O(1)
空间复杂度：O(1)

[back to Catalogue](#Catalogue)

-------------------------
## <a name="771"> 771. Jewels and Stones
### Question:
>You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".

### Example:

>Example 1:

Input: J = "aA", S = "aAAbbbb"
Output: 3
Example 2:

Input: J = "z", S = "ZZ"
Output: 0

### Thinking:
>too easy

### Solution:

```python
class Solution:
    def numJewelsInStones(self, J: str, S: str) -> int:
        J = list(J)
        # S = list(S)
        num = 0
        for i in J:
            num += S.count(i)
        return num
```
-------------------------