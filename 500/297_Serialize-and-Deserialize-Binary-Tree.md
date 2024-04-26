# 297. 二叉树的序列化与反序列化

[[2024-04-24]]

left 和 right 的判断冗余，代码可以压缩。

```python
class Codec:

    def serialize(self, root):
        if not root:
            return ""

        queue = [root]
        items = [str(root.val)]
        while queue:
            x = queue.pop(0)

            if x.left:
                items.append(str(x.left.val))
                queue.append(x.left)
            else:
                items.append("null")

            if x.right:
                items.append(str(x.right.val))
                queue.append(x.right)
            else:
                items.append("null")

        return ",".join(items)

    def deserialize(self, data):
        if not data:
            return None
        items = data.split(",")
        head = TreeNode(items[0])
        queue = [head]
        i = 1
        while queue:
            x = queue.pop(0)
            if i < len(items):
                if items[i] != "null":
                    x.left = TreeNode(int(items[i]))
                    queue.append(x.left)
                i += 1
            if i < len(items):
                if items[i] != "null":
                    x.right = TreeNode(int(items[i]))
                    queue.append(x.right)
                i += 1
        return head
```
