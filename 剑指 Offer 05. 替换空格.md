# 剑指 Offer 05. 替换空格

## Description

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

 

示例 1：

输入：s = "We are happy."
输出："We%20are%20happy."


限制：

0 <= s 的长度 <= 10000



## Solution

```java
class Solution {
    public String replaceSpace(String s) {
        // Expand the original char array then copy
        
        int count = 0; // count the appearance of space
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                count++;
            }
        }

        char[] arr = new char[s.length() + 2 * count];
        
        // populate the new array
        int index = 0; // for iterating the original string
        int i = 0; // for populating the new string
        while (index < s.length()) {
            if (s.charAt(index) == ' ') {
                arr[i++] = '%';
                arr[i++] = '2';
                arr[i++] = '0';
            } else {
                arr[i++] = s.charAt(index);
            }
            
            index++;
        }

        return new String(arr);
    }
}
```

- TC: O(n)
- SC: O(n)