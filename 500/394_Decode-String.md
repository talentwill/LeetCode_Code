# 394. 字符串解码

[[2024-04-20]]

```python
class Solution:

    def decodeString(self, s: str) -> str:
        items = list(x for x in re.split("(\])|\[", s) if x)
        pattern = r"([a-z]*)(\d*)"

        items2 = []
        for x in items:
            if x != r"]":
                items2.extend([x for x in re.match(pattern, x).groups() if x])
            else:
                items2.append(x)

        stk = [""]
        for x in items2:
            if x == r"]":
                s1 = stk.pop()
                s2 = stk.pop()

                s2 = int(s2) * s1

                if stk[-1].isdigit():
                    stk.append(s2)
                else:
                    stk[-1] += s2

            elif x.isdigit():
                stk.append(x)
            else:
                if stk[-1].isdigit():
                    stk.append(x)
                else:
                    stk[-1] += x
        return "".join(stk)
```
