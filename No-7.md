https://leetcode-cn.com/problems/reverse-integer/

```c++
class Solution {
public:
    int reverse(int x) {
        bool flag = x > 0 ? true : false;
        long tem = x;
        if (!flag) {
            tem *= -1;
        }
        vector<int> v;
        while (tem > 0) {
            v.push_back(tem % 10);
            tem /= 10;
        }
        vector<int>::iterator it;
        long result = 0;
        for (it = v.begin(); it != v.end(); it++) {
            result = result * 10 + *it;
        }
        if (result > INT_MAX) {
            return 0;
        }
        if (!flag) {
            result *= -1;
        }
        if (result < INT_MIN) {
            return 0;
        }
        return result;
    }
};
```
