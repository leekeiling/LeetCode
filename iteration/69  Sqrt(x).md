### 69  Sqrt(x)

Implement `int sqrt(int x)`.

Compute and return the square root of *x*, where *x* is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

**Example 1:**

```
Input: 4
Output: 2

```

**Example 2:**

```c++
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```

#### 【基本思路】

二分法查找符合条件的数。注意有越界的问题，所以对于$ x* x > y$ 的判断我们转化成 $ x > y/x$

```c++
class Solution {
public:
    int mySqrt(int x) {
    	int l = 0, r = x, mid = x;
    	while(true){
    		if(mid !=0 && mid > x/mid){
    			r = mid - 1;
    			mid = (l+r)/2;
			}else{
				if((mid+1) > x/(mid+1)){
					return mid;
				}
				l = mid + 1;
				mid = (l + r)/2;
			}
		}
    }
};
```

