##  409 Longest Palindrome

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example `"Aa"` is not considered a palindrome here.

**Note:**
Assume the length of given string will not exceed 1,010.

**Example:**

```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

#### **【基本思想】**

使用哈希映射，将所有单词映射到一个数组中，由于偶数偶数个的单词才能组成回文串（先不考虑中间的单词情况），所以需要将数组中的奇数减一。如果存在奇数，可以将一个单词放置回文串的中间。

```c++
class Solution {
public:
    int longestPalindrome(string s) {
        int arr[256] = {};
        int res = 0; 
        for(int i = 0; i < s.size(); i++){
        	arr[s[i] - '0']++;
		}
		for(int i = 0; i < 256; i++){
			res += arr[i]/2 * 2;  //奇数的化减一，使所有数据都为偶数 
		}
		if(res < s.size()) res++;
		return res;
    }
};
```

