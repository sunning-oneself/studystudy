1. 给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。


```java
public class Te {


    public static void main(String[] args) {
        String s = "bbbbb2";
        int  subLen = 0, n = s.length();
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (int i = 0, j=0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            subLen = Math.max(subLen, j-i);
            map.put(s.charAt(j), j);
        }
        System.out.println(subLen);
//		return subLen;
    }

}

```

2. 删除排序链表中的重复元素


3. 两数之和

```java
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            int other = target - nums[i];
            if (map.containsKey(other)){
                return new int[]{map.get(other), i};
            }
            map.put(nums[i], i);
        }
        throw new IllegalArgumentException("no num");
    }
```

