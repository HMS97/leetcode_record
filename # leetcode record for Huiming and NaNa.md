# leetcode record for Huiming and NaNa

### <a name="Catalogue"/>Catalogue

* Easy
    * [2. 整数反转](#2)
    

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

作者：boywithacoin_cn
链接：https://leetcode-cn.com/problems/reverse-integer/solution/pythondan-chu-he-tui-ru-shu-zi-yi-chu-qian-jin-xin/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


```

[back to Catalogue](#Catalogue)

-------------------------