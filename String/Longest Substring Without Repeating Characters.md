```c++
class Solution{
public:
    int lengthOfLongestSubstring(string s) {
    	vector<char> v;
    	int max_length = 0;
        for(int i=0;i<s.size();i++){
        	vector <char>::iterator it;
			for(it=v.begin();it!=v.end();it++){
				if(s[i]==*it){
					v.erase(v.begin(),it+1);
					break;
				}
			} 
			v.push_back(s[i]);
			if(v.size()>max_length){
				max_length = v.size();
			}
		}
		return max_length; 
    }
};
```

