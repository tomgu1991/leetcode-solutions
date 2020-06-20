//
// Created by g00522859 on 2020/4/11.
//

#ifndef CPP_PRIMER_LEETCODE_5_H
#define CPP_PRIMER_LEETCODE_5_H

#include <string>
using namespace std;

class LeetCode_5 {
    public:
    string check3(string s, int index) {
        int center = index;
        int size = 0;
        int Max = s.size();
        while (true) {
            if ((center - size) >= 0 && (center + size) <= Max) {
                if (s[center - size] == s[center + size]) {
                    size++;
                } else {
                    break;
                }
            } else {
                break;
            }
        }
        return s.substr(center - (size - 1), 2 * (size-1) + 1);
    }

    string check2(string s, int index) {
        int start = index;
        int Max = s.size();
        if (index + 1 > Max) {
            return s.substr(index, 1);
        }
        int end = index + 1;
        if (s[start] != s[end]) {
            return s.substr(index, 1);
        }
        while (true) {
            if ((start - 1) >= 0 && (end + 1) <= Max) {
                if (s[start - 1] == s[end + 1]) {
                    start--;
                    end ++;
                }else {
                    break;
                }
            } else {
                break;
            }
        }
        return s.substr(start, end - start + 1);
    }

    string longestPalindrome(string s) {
            int size = s.size();
            if (size == 0) return "";
            if (size == 1) return s;
            string result = "";
            for (int index = 0; index < size; index++) {
                string tem = check3(s, index);
                result = result.size() < tem.size() ? tem : result;
                tem = check2(s, index);
                result = result.size() < tem.size() ? tem : result;
                if (result.size() == size) {
                    return result;
                }
            }
            return result;
        }

};


#endif //CPP_PRIMER_LEETCODE_5_H
