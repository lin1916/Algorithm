[[原题链接]](https://leetcode.cn/problems/implement-strstr/) 实现 strStr()函数。

给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串出现的第一个位置（下标从 0 开始）。如果不存在，则返回  `-1` 。

说明：

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与 C 语言的 `strstr()` 以及 `Java` 的 `indexOf()` 定义相符。

 

示例 1：
```
输入：haystack = "hello", needle = "ll"
输出：2
```

示例 2：
```
输入：haystack = "aaaaa", needle = "bba"
输出：-1
```

提示：
- `1 <= haystack.length, needle.length <= 104`
- `haystack` 和 `needle` 仅由小写英文字符组成

关键字：KMP算法、next数组

代码：

方法一：KMP算法
```cpp
class Solution {
public:
    int strStr(string haystack, string needle) 
    {
        // int left = 0, right = 0;
        // for (; left < haystack.size() && right < needle.size();)
        // {
        //     if (haystack[left] != needle[right])
        //     {
        //         left++;
        //         right = 0;
        //     }
        //     else 
        //     {
        //         left++;
        //         right++;
        //     }
        // }
        // if (right == needle.size())
        //     return left-right;
        // else
        //     return -1;
        int j = 0;
        vector<int> next (needle.size(), 0);

        for (int i = 1; i < needle.size(); i++)
        {
            while (j > 0 && needle[i] != needle[j])
                    j = next[j-1];
            if (needle[i] == needle[j])
            {
                j++;
            }
            
            
            next[i] = j;
        }

        for (int i = 0, m = 0; i < haystack.size(); i++)
        {
            while (m > 0 && haystack[i] != needle[m])
            {
                m = next[m-1];
            }
            if (haystack[i] == needle[m])
            {
                m++;
            }
            if (m == needle.size())
                return (i - needle.size()+1);
        }
        return -1;
    }
        
};
```
