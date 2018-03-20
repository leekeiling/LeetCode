```c++
//There are two sorted arrays nums1 and nums2 of size m and n respectively.
//Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

//Solution:
//Try to traverse two arrays simutaneously according to their compared result;
//For example:
//array1: 0 4 5
//array2: 2 5 3
//position in both arrays is 0 at the beginning. array1[0]<array2[0], array1's position moves to 1, and 
//array's position remain still.

class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
		vector<int> v; 
	    int m=nums1.size(), n=nums2.size();
		while(!nums1.empty() && !nums2.empty()){
			int num=0;
			if(nums1[0] > nums2[0]){
				num = nums2[0];
				nums2.erase(nums2.begin());
			}
			else{
				num = nums1[0];
				nums1.erase(nums1.begin());
			}
			v.push_back(num);
		}		 		 
		while(!nums1.empty()){
			v.push_back(nums1[0]);
			nums1.erase(nums1.begin());
		}
		while(!nums2.empty()){
			v.push_back(nums2[0]);
			nums2.erase(nums2.begin());
		}
		if((m+n)%2==0){
			return (v[(m+n)/2] + v[(m+n)/2-1])*1.0/2.0;
		}else{
			return v[(m+n)/2]*1.0;
		}
    }
};
```

