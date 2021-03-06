## 665 Non-decreasing Array

Given an array with `n` integers, your task is to check if it could become non-decreasing by modifying **at most** `1` element.

We define an array is non-decreasing if `array[i] <= array[i + 1]` holds for every `i` (1 <= i < n).

**Example 1:**

```
Input: [4,2,3]
Output: True
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.

```

**Example 2:**

```
Input: [4,2,1]
Output: False
Explanation: You can't get a non-decreasing array by modify at most one element.
```

### 【基本思路】

**遍历，修改尽量减少对后续数字的修改**。

在出现 nums[i] < nums[i - 1] 时，需要考虑的是应该修改数组的哪个数，使得本次修改能使 i 之前的数组成为非递减数组，并且 **不影响后续的操作** 。优先考虑令 nums[i - 1] = nums[i]，因为如果修改 nums[i] = nums[i - 1] 的话，那么 nums[i] 这个数会变大，就有可能比 nums[i + 1] 大，从而影响了后续操作。还有一个比较特别的情况就是 nums[i] < nums[i - 2]，只修改 nums[i - 1] = nums[i] 不能使数组成为非递减数组，只能修改 nums[i] = nums[i - 1]。

```c++
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
    	int cnt = 0, size = nums.size();
  		for(int i = 1; i < nums.size(); i++) {
  			if(nums[i-1] > nums[i]){
                cnt++;
				if(i - 2 >= 0 && nums[i] < nums[i-2]) {
                    nums[i] = nums[i-1];
                }
                else {
                    nums[i-1] = nums[i];
                }
			}
		}      
		return cnt<=1;
    }
};

```

