#### 77 Combinations

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.

**Example:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```c++
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> ans;
        vector<int> v;
        DFS(1, k, v, ans, n);
        return ans;
    }
    
private:
	void DFS(int begin, int cnt, vector<int>& v, vector<vector<int> >& ans, int n){
		if(cnt==0){
			ans.push_back(v);
            return;
		}
		for(int i=begin;i<=n;i++){
			v.push_back(i);
			DFS(i+1, cnt-1, v, ans, n);
			v.pop_back();
		}
	}
};
```

