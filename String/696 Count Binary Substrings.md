### 696 Count Binary Substrings

Give a string `s`, count the number of non-empty (contiguous) substrings that have the same number of 0's and 1's, and all the 0's and all the 1's in these substrings are grouped consecutively.

Substrings that occur multiple times are counted the number of times they occur.

**Example 1:**

```
Input: "00110011"
Output: 6
Explanation: There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".

Notice that some of these substrings repeat and are counted the number of times they occur.

Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.

```

**Example 2:**

```
Input: "10101"
Output: 4
Explanation: There are 4 substrings: "10", "01", "10", "01" that have equal number of consecutive 1's and 0's.

```

**Note:**

`s.length` will be between 1 and 50,000.

`s` will only consist of "0" or "1" characters.

#### 【基本思路】

观察到其实可以把字符串s转化为0和1的堆。譬如，“1111000011010001011”转化为“4 4 2 1 1 3 1 1 2 ”，也就是统计一下每个连续子串的个数，这样我们就可以方便的获得满足条件的子串个数，统计转化后的数组相邻元素之间最小的那个求和即可

```c++
class Solution {
public:
    int countBinarySubstrings(string s) {
    	int arr[100000] = {0};
    	int cnt = 0, res = 0;
        for(int i = 0; i < s.size(); i++){
    		arr[cnt]++;
    		if(i+1 != s.size() && s[i] != s[i+1])	cnt++;
		} 
        cnt++;
		for(int i = 1; i < cnt; i++) {
			res += min(arr[i], arr[i-1]);
		}
		return res;
    }
};
```



#### 【基本思路二】

利用pre指针和cur指针。

其实可以把这部分额外的空间给释放出来，我们看下面这段代码，不仅空间复杂度为常数，而且时间复杂度也稍有提升.

```c++
class Solution {
public:
    int countBinarySubstrings(string s) {
    	int i = 0, pre = -1, res = 0;
    	while(i < s.size()) {
    		int j = i;
    		while(i+1 != s.size() && s[i] == s[i+1])  i++;
            i++;
    		int cur = i - j;
    		if(pre!=-1)	res += min(pre, cur);
    		pre = cur;
		}
		return res;
	}
};
```

