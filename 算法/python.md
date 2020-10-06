1. 最大连续子数组的和


```python
def f(nums):
	for i in range(1, len(nums)):
		nums[i] += max(nums[i-1], 0)
	return max(nums)

```

2. 链表中是否有环


```python
def has_cycle(head):
	slow = fast = head
	while slow and fast and fast.next:
		slow = slow.next
		fast = fast.next.next
		if slow is fast:
			return True
	return False
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

9. 删除有序链表中的重复元素

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

13. 冒泡排序

```
def bubbleSort(arr):
    n = len(arr)

    # 遍历所有数组元素
    for i in range(n):

        # Last i elements are already in place
        for j in range(0, n-i-1):

            if arr[j] > arr[j+1] :
                arr[j], arr[j+1] = arr[j+1], arr[j]
```

14. 求数组中是否存在3个数之和等于N

15. 两个链表是否相交

```python
def judge_x(pHead1, pHead2):
    if not pHead1 or not pHead2 or not pHead1.next or not pHead2.next:
        return None
    hashset = set()
    p = pHead1  # 用来遍历链表
    hashset.add(p)
    while p.next:
        p = p.next
        hashset.add(p)
        # 这里注意要你把所有的节点都存储到hashset中

    p = pHead2
    while p:
        if p.next in hashset:
            return True
        p = p.next
    return False
```

16. 最长非重复子串

```python
def dup(s):
	u = ''
	res = 0
	for i in s:
		if i not in u:
			u += i
			res = max(len(u), res)
		else:
			index = u.find(i)
			u = u[index+1:]+i
	return res
```

17. 最长公共子序列

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m = len(text1)
        n = len(text2)
        C = [[0 for i in range(n+1)] for j in range(m+1)]
        for i in range(1, m+1):
            for j in range(1, n+1):
                if text1[i-1] == text2[j-1]:
                    C[i][j] = C[i-1][j-1] + 1
                else:
                    if C[i-1][j] > C[i][j-1]:
                        C[i][j] = C[i-1][j]
                    else:
                        C[i][j] = C[i][j-1]
        return C[-1][-1]

```

18. 遍历一次删除倒数第k个节点

```python
    def deln(head, n):
	if head is None:
		return False
	p = head
	
	for i in range(n):
		print('1111')
		if p.next is not None:
			print(p.val)
			p = p.next
		else:
			return False
	q = head
	while p.next:
		p = p.next
		q = q.next
	print(q.next.val)
	q.next = q.next.next
	return True
```

19. 将一个列表中的元素组合成最大的数(列表中的元素全是整数)

```python
def max_sort(l):
	n = len(l)
	for i in range(n-1):
		for j in range(n-1-i):
			if str(l[j]) + str(l[j+1]) < str(l[j+1]) + str(l[j]):
				l[j], l[j+1] = l[j+1], l[j]
	s = ''
	for k in l:
		s += str(k)
	return s
```

20. 最长公共子串

```python
def sub(s1,s2):
	m = len(s1)
	n = len(s2)
	f = [[0 for i in range(n+1)] for j in range(m+1)]
	print(f)
	max_sub = 0

	for i in range(1,m+1):
		for j in range(1,n+1):
			if s1[i-1] == s2[j-1]:
				f[i][j] = f[i-1][j-1] + 1
				if max_sub < f[i][j]:
					max_sub = f[i][j]
	return max_sub
```
