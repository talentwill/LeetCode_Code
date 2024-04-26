# 946. 验证栈序列

[[2024-04-24]]

不需要判断 `j` 越界，最后保证 `stk` 是空的。

```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        stk = []
        j = 0
        for i in pushed:
            stk.append(i)
            while j < len(popped) and stk and popped[j] == stk[-1]:
                stk.pop()
                j += 1
        return j == len(popped)
```
