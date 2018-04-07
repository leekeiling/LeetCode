# 34、Search for a Range

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

For example,
Given `[5, 7, 7, 8, 8, 10]` and target value 8,
return `[3, 4]`.

#### 【思路】

二分查找，递归。

二分查找搜索一个记录时，当分割点即是需要搜索的记录时，二分查找停止搜索；

本题类似与二分查找，但是要将序列一直分割，分割过程中比较分割点与target value，更新target value的上界和下界。

#### 【代码】

```c++
class Solution {
public:
	int bottom = 1000000, top = -1;
    vector<int> searchRange(vector<int>& nums, int target) {
    	if(nums.size()==0){
    		 return vector<int>{-1,-1};
		}
        int l = 0;
        int r = nums.size() - 1;
        search(l, r, nums, target);
		if(top==-1)  return vector<int>{-1,-1};
		return vector<int>{bottom, top};  
    }
private:
	void search(int l, int r, vector<int>& nums, int target){
		if(l > r) return;
		int mid = (l+r)/2;
		if(nums[mid] == target) {
			cout<<nums[mid]<<endl;
			if(mid < bottom) {
				bottom = mid;
			}
			if(mid > top){
				top =  mid;
			}
		}
		search(l, mid-1, nums, target);
		search(mid+1, r, nums, target);
	}
};
```

