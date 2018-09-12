### 567. 字符串的排列
给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。
换句话说，第一个字符串的排列之一是第二个字符串的子串。
```
示例1:
输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").
 
示例2:
输入: s1= "ab" s2 = "eidboaoo"
输出: False
```
算法思想：滑动窗口机制


```C++
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        vector<int> str1(26);
        vector<int> str2(26);
        int len1 = s1.length();
        int len2 = s2.length();
        
        if(s1.length() == 0)
            return true;
        if(s2.length() == 0)
            return false;
        for(int i = 0; i < len1; i++)
        {
            str1[s1[i] - 'a'] ++;
            str2[s2[i] - 'a'] ++;
        }
        if(str1 == str2)
            return true;
        for(int i = 0; i + len1 < len2; i++)
        {
            str2[s2[i] - 'a'] --;//去掉首部
            str2[s2[i + len1] - 'a'] ++;//加入尾部，相当于向后移动一个单位
            if(str1 == str2)
                return true;
        }
        return false;
    }
};
```