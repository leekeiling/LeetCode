

需要考虑整数反转后溢出的情况。

这题有点坑，没说明溢出时返回0；

```c++
class Solution {
public:
    int reverse(int x) {
        int a = abs(x), m = 0, n = 0, reverse_num = 0;
        string arr=""; 
        while(a){
        	stringstream ss;
        	ss << a % 10;
        	arr += ss.str();
        	a /= 10;
        	m++;
		}
		while(arr[n] == '0'){
			n++;
		}	
		while(n<m){
			reverse_num += (arr[n] - '0') * pow(10, (m-n-1));
			n++;
		}
		if(reverse_num < 0) return 0;
		if(x<0)  return -reverse_num;
		else return reverse_num;
    }
};
```

