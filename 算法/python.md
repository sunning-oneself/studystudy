1. 最大连续子数组的和


```python
def max_sum(l):
    if not l:
	return
    m = l[0]
    s = l[0]
    for i in l:
	if i <=0:
	    s = i
	else:
       	    s += i
	m = max(s, m)
    return m
```

2. 求数组最大连续子序列和


```python

def sub_sum(l):
    if not l:
        return
    max_sum = l[0]
    pre_sum = 0
    for i in l:
        if pre_sum < 0:
            pre_sum = i
        else:
            pre_sum += i
        if pre_sum > max_sum:
            max_sum = pre_sum
    return max_sum

```


3. 写一个单例模式，什么时候用到，还了解哪些设计模式，装饰者模式是什么，举例

```python
class Singleton():
    _lock = threading.Lock()
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, "_instance"):
            with Singleton._lock:
                if not hasattr(cls, "_instance"):
                    Singleton._instance = super().__new__(cls, *args, **kwargs)
        return Singleton._instance
```

	1、生成全局惟一的序列号；
	2、访问全局复用的惟一资源，如磁盘、总线等；
	3、单个对象占用的资源过多，如数据库等；
	4、系统全局统一管理，如Windows下的Task Manager；
	5、网站计数器。

4. 单链表旋转

```python
class Node():
    def __init__(self, val):
        self.val = val
        self.next = None

def reverse_list(head):
    if not head or not head.next:
        return head
    new_head = reverse_list(head.next)
    head.next.next = head
    head.next = None
    return new_head
```

5. 找出字符数组中只出现三次，且最早出现完三次的字符

6. 快排

```python
def quick_sort(l, start, end):
    if start >= end:
        return l
    left = start
    right = end
    mid = l[left]
    while left < right:
        while left < right and l[right] > mid:
            right -= 1
        l[left] = l[right]
        while left < right and l[left] <= mid:
            left += 1
        l[right] = l[left]
    l[left] = mid
    quick_sort(l, start, left-1)
    quick_sort(l, left+1, end)

if __name__ == "__main__":
    l = [1,2,1,2,2,4,1,3]
    quick_sort(l, 0, len(l)-1)
    print(l)

```

7. 合并两个有序链表

```python

class Solution:
    def mergeTwoLists(self, l1, l2):
        if l1 is None:
            return l2
        elif l2 is None:
            return l1
        elif l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2

```

8. 合并两个有序列表


```python

def hebing(list1,list2):
    result=[]
    while list1 and list2:
        if list1[0]<list2[0]:
            result.append(list1[0])
            del list1[0]
        else:
            result.append(list2[0])
            del list2[0]
    if list1:
        result.extend(list1)
    if list2:
        result.extend(list2)
    return result

```

9. 删除排序链表中的重复元素

```python
def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return None
        cur_List = head
        while cur_List.next:
            if cur_List.val == cur_List.next.val:
                cur_List.next = cur_List.next.next
            else:
                cur_List = cur_List.next
        return head
```

9. 两个数组的交集

10. 二叉搜索树公共祖先

```python
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        # Value of current node or parent node.
        parent_val = root.val

        # Value of p
        p_val = p.val

        # Value of q
        q_val = q.val

        # If both p and q are greater than parent
        if p_val > parent_val and q_val > parent_val:
            return self.lowestCommonAncestor(root.right, p, q)
        # If both p and q are lesser than parent
        elif p_val < parent_val and q_val < parent_val:
            return self.lowestCommonAncestor(root.left, p, q)
        # We have found the split point, i.e. the LCA node.
        else:
            return root

```

11. 字符串中的第一个唯一字符

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        """
        :type s: str
        :rtype: int
        """
        # build hash map : character and how often it appears
        count = collections.Counter(s)

        # find the index
        for idx, ch in enumerate(s):
            if count[ch] == 1:
                return idx
        return -1
```

12. 二分查找

```python
def binary_chop(alist, data):
    """
    递归解决二分查找
    :param alist:
    :return:
    """
    n = len(alist)
    if n < 1:
        return False
    mid = n // 2
    if alist[mid] > data:
        return binary_chop(alist[0:mid], data)
    elif alist[mid] < data:
        return binary_chop(alist[mid+1:], data)
    else:
        return True
```
