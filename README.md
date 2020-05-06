# leetcode record for Huiming and NaNa

## <a name="Catalogue"/>Catalogue
I love nana
* Easy
    * [1. Two Sum](#1)
    * [2. 整数反转](#2)

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

    

## <a name="2"> 2. 整数反转
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