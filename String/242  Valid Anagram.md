## 242  Valid Anagram

Given two strings *s* and *t*, write a function to determine if *t* is an anagram of *s*.

For example,
*s* = "anagram", *t* = "nagaram", return true.
*s* = "rat", *t* = "car", return false.

**Note:**
You may assume the string contains only lowercase alphabets.

#### 【基本思想】

字符串只包含小写字符，总共有 26 个小写字符。可以用 Hash Table 来映射字符与出现次数，因为键值范围很小，因此可以使用长度为 26 的整型数组对字符串出现的字符进行统计，然后比较两个字符串出现的字符数量是否相同。

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int arr1[26] = {0};
		int arr2[26] = {0};
		for(int i = 0; i < s.size(); i++){
			arr1[s[i] - '0' - 49]++;
		} 
		for(int i = 0; i < t.size(); i++){
			arr2[t[i] - '0' - 49]++;
		}
		for(int i = 0; i < 26; i++){
			if(arr1[i] != arr2[i])	return false;
		}
		return true;
    }
};
```

