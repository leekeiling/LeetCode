## 763 Partition Labels

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example 1:**

```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.

```

**Note:**

1. `S` will have length in range `[1, 500]`.
2. `S` will consist of lowercase letters (`'a'` to `'z'`) only.



### 【基本思想】

题意是要对一个字符串进行尽可能多的划分，并保证每个划分中的元素不在其他划分中出现。

想法比较具有技巧性。如果一段序列中每个元素的在S中最右边的序号都在某个范围内，那么就可以划分成一个段。

因此，使用字典保存每个元素出现的最靠右的位置。然后对字符串S进行遍历，找出最靠右的序号的最大值j。如果i和j重合了，说明已经到了这个划分的末尾了，然后进行划分。并开始计算下一个划分。

```c++
class Solution {
public:
    int divide(string S, int start, int end, int letterRight[26])
    {
    	int left, right;
    	left = start;
    	right = letterRight[S[left] - 'a'];
    	for (int i = left+1; i <= right; i++)
    	{
			if (letterRight[S[i] - 'a'] > right) right = letterRight[S[i] - 'a'];
		} 
		return right - left + 1;
	}
	vector<int> partitionLabels(string S) {
		int letterRight[26];
		vector<int> result;
		
		for (int i = 0; i < 26; i++)
		{
			int t = S.find_last_of((char)(i + 'a'));
			letterRight[i] = t;
		}
		int start = 0; int end = S.size(); int tmp;
		while (start < end)
		{
			tmp = divide(S, start, end, letterRight);
			result.push_back(tmp);
			start += tmp;
		}
		return result;
    }
};
```

