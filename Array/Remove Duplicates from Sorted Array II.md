80. ### Remove Duplicates from Sorted Array II

Given a sorted array *nums*, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most *twice* and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example 1:**

```
Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.

```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

#### 【基本思路】

首先需要判断一个元素重现次数是否大于2，如果大于2那么多余的元素的位置作为占位符，需要被其他新的元素填充。为了让新的元素填充到合适的位置，需要一个辅助空间cnt来保存每个元素需要向左移动的位数。

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
    	int cnt = 0;
        for(int i =  2; i < nums.size(); i++){
        	if(nums[i] == nums[i-2-cnt]){
        		cnt++;
			}
			else{
				nums[i - cnt] = nums[i];
			}
		}
		return nums.size() - cnt;
    }
};
```

