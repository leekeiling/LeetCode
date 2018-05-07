### 9 Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true

```

**Example 2:**

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

```

**Example 3:**

```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

#### 【基本思路】

题目要求：不能使用额外空间，也就不能将整数转换为字符串进行判断。

将整数分成左右两部分，右边那部分需要转置，然后判断这两部分是否相等。

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        if(x == 0)	return true;
        if(x < 0)	return false;
        if(x % 10 == 0)	return false;
        int right = 0;
        while(right < x){
        	right = x % 10 +  right * 10;
        	x /= 10;
		}
		return right == x || right/10 == x;
    }
};
```

