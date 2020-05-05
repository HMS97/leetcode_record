# leetcode record for Huiming and NaNa

## <a name="Catalogue"/>Catalogue
I love nana
* Easy
    * [1. Two Sum](#1)

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