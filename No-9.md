https://leetcode-cn.com/problems/palindrome-number/

```c++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x == 0) return true;
        if (x < 0) return false;
        
        vector<int> end;
        while (x > 0) {
            int tem = x % 10;
            x = x / 10;
            end.push_back(tem);
        }
        
        vector<int> front(end);
        std::reverse(front.begin(), front.end());
        for (int i = 0; i < front.size(); i++) {
            if (front[i] != end[i]) {
                return false;
            }
        }
        return true;
    }
};
```
