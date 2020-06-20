//
// Created by g00522859 on 2020/4/13.
//

#ifndef CPP_PRIMER_LEETCODE_20_H
#define CPP_PRIMER_LEETCODE_20_H
#include <stack>
#include <string>
using namespace std;

class LeetCode_20 {
public:
    bool match(stack<char> &stack, char &source) {
        char target = stack.top();
        switch (source) {
            case ']':
                if (target != '[') {
                    return false;
                }
                break;
            case '}':
                if (target != '{') {
                    return false;
                }
                break;
            case ')':
                if (target != '(') {
                    return false;
                }
                break;
            default:
                return false;
        }
        stack.pop();
        return true;
    }

    bool isValid(string s) {
        stack<char> container;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '{' || s[i] == '(' || s[i] == '[') {
                container.push(s[i]);
            } else {
                if (!match(container, s[i])) {
                    return false;
                }
            }
        }
        return true;
    }
};
#endif //CPP_PRIMER_LEETCODE_20_H


//
// Created by g00522859 on 2020/4/14.
//

#ifndef CPP_PRIMER_LEETCODE_21_H
#define CPP_PRIMER_LEETCODE_21_H

struct ListNode {
int val;
ListNode *next;
ListNode(int x) : val(x), next(nullptr) {}
};

class LeetCode_21 {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1 == nullptr) return l2;
        if (l2 == nullptr) return l1;
        ListNode *ptr;
        ListNode *head;
        if (l1->val < l2->val) {
            ptr = new ListNode(l1->val);
            l1 = l1->next;
        } else {
            ptr = new ListNode(l2->val);
            l2 = l2->next;
        }
        head = ptr;
        ListNode *tem;
        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val < l2->val) {
                tem = new ListNode(l1->val);
                l1 = l1->next;
            } else {
                tem = new ListNode(l2->val);
                l2 = l2->next;
            }
            ptr->next = tem;
            ptr = tem;
        }
        // left
        while (l1 != nullptr) {
            tem = new ListNode(l1->val);
            l1 = l1->next;
            ptr->next = tem;
            ptr = tem;
        }
        while (l2 != nullptr) {
            tem = new ListNode(l2->val);
            l2 = l2->next;
            ptr->next = tem;
            ptr = tem;
        }
        return head;

    }
};
#endif //CPP_PRIMER_LEETCODE_21_H


//
// Created by g00522859 on 2020/4/14.
//

#ifndef CPP_PRIMER_LEETCODE_26_H
#define CPP_PRIMER_LEETCODE_26_H

#include <vector>
using namespace std;

class LeetCode_26 {
public:
    int removeDuplicates(vector<int>& nums) {
        int cur = 0, ptr = 0;
        if (nums.size() == 0) return cur;
        ptr++;
        while (ptr < nums.size()) {
            if (nums[ptr] == nums[cur]) {
                ptr++;
            } else {
                cur++;
                nums[cur] = nums[ptr];
                ptr++;
            }
        }
        return cur + 1;
    }
};

#endif //CPP_PRIMER_LEETCODE_26_H


//
// Created by g00522859 on 2020/4/14.
//

#ifndef CPP_PRIMER_LEETCODE_28_H
#define CPP_PRIMER_LEETCODE_28_H

#include <string>
using namespace std;

class LeetCode_28 {
public:
    int strStr(string haystack, string needle) {
        if (needle == "") {
            return 0;
        }
        if (haystack == "") {
            return -1;
        }
        if (haystack.size() < needle.size()) {
            return -1;
        }
        int result = -1;
        for (int i = 0; i < haystack.size() - needle.size() + 1; i++) {
            if (haystack[i] == needle[0] && has(i, haystack, needle) > -1) {
                return i;
            }
        }
        return result;
    }

    int has(int index, string &source, string &target) {
        for (int i = 1; (i + index) < source.size() && (i < target.size()); i++) {
            if (source[i + index] != target[i]) {
                return -1;
            }
        }

        return index;
    }
};

#endif //CPP_PRIMER_LEETCODE_28_H


//
// Created by g00522859 on 2020/4/15.
//

#ifndef CPP_PRIMER_LEETCODE_35_H
#define CPP_PRIMER_LEETCODE_35_H

#include <vector>
#include <algorithm>

using namespace std;

class LeetCode_35 {
public:
    int mysearch(vector<int> &nums, int target, int start, int end) {
        if (start == end) {
            if (target == nums[start]) return start;
            else if (target < nums[start]) return start;
            else start + 1;
        }
        if (start + 1 == end) {
            if (target <= nums[start]) return start;
            else if (target >= nums[end]) return end;
            else return start + 1;
        }
        int mid = (start + end) / 2;
        if (target == nums[mid]) return mid;
        if (target > nums[mid]) return mysearch(nums, target, mid + 1, end);
        else return mysearch(nums, target, start, mid);
    }

    int searchInsert(vector<int>& nums, int target) {
        if (nums.size() == 0) {
            return 0;
        }
        if (target < nums[0]) {
            return 0;
        }
        if (target > nums[nums.size()-1]) {
            return nums.size();
        }
        return mysearch(nums, target, 0, nums.size());
    }
};

#endif //CPP_PRIMER_LEETCODE_35_H


//
// Created by g00522859 on 2020/4/16.
//

#ifndef CPP_PRIMER_LEETCODE_38_H
#define CPP_PRIMER_LEETCODE_38_H

#include <vector>
#include <string>
using namespace std;

class LeetCode_38 {
public:
    string buildFrom(vector<int> &v) {
        string str = "";
        for (int i = 0; i < v.size(); i++) {
            str += static_cast<char>(v[i] + '0');
        }
        return str;
    }

    vector<int> nextVector(vector<int> v) {
        vector<int> next;
        int cur = v[0];
        int count = 1;
        for (int i = 1; i < v.size(); i++) {
            if (v[i] == cur) {
                count++;
            } else {
                next.push_back(count);
                next.push_back(cur);
                cur = v[i];
                count = 1;
            }
        }
        next.push_back(count);
        next.push_back(cur);
        return next;
    }

    string countAndSay(int n) {
        if (n == 1) return "1";
        vector<int> v = {1};
        for (int index = 2; index <= n; index++) {
            v = nextVector(v);
        }
        return buildFrom(v);
    }
};

#endif //CPP_PRIMER_LEETCODE_38_H


//
// Created by g00522859 on 2020/4/18.
//

#ifndef CPP_PRIMER_LEETCODE_58_H
#define CPP_PRIMER_LEETCODE_58_H

#include <string>
#include <cctype>
#include <vector>

using namespace std;

class LeetCode_58 {
public:
    int lengthOfLastWord(string s) {
        if (s.empty()) return 0;
        int count = 0;
        vector<int> bags;
        for (int i = 0; i < s.size(); i++) {
            if (isalpha(s[i])) {
                count++;
            } else {
                if (count != 0)
                    bags.push_back(count);
                count = 0;
            }
        }
        if (count != 0) bags.push_back(count);
        if (bags.size() == 0) return 0;
        return bags[bags.size() - 1];
    }
};

#endif //CPP_PRIMER_LEETCODE_58_H


//
// Created by g00522859 on 2020/4/21.
//

#ifndef CPP_PRIMER_LEETCODE_66_H
#define CPP_PRIMER_LEETCODE_66_H
#include <vector>
#include <algorithm>
using std::vector;
using std::reverse;

class LeetCode_66 {
public:
    vector<int> plusOne(vector<int>& digits) {
        int loc = digits.size() - 1;
        int add = 1;
        vector<int> result;
        while (loc >= 0) {
            if (digits[loc] + add >= 10) {
                result.push_back(digits[loc] + add - 10);
                add = 1;
            } else {
                result.push_back(digits[loc] + add);
                add = 0;
            }
            loc--;
        }
        if (add == 1) {
            result.push_back(add);
        }
        reverse(result.begin(), result.end());
        return result;
    }
};
#endif //CPP_PRIMER_LEETCODE_66_H


//
// Created by g00522859 on 2020/4/12.
//

#ifndef CPP_PRIMER_LEETCODE_122_H
#define CPP_PRIMER_LEETCODE_122_H

#include <vector>
using namespace std;

class LeetCode_122 {
public:
    int maxProfit(vector<int>& prices) {
        vector<int> diff;
        for (int index = 0; index < prices.size() - 1; index++) {
            diff.push_back(prices[index + 1] - prices[index]);
        }
        int sum = 0;
        int delta = 0;
        for (int index = 0; index < diff.size(); index++) {
            if (diff[index] < 0) {
                sum += delta;
                delta = 0;
            } else {
                delta += diff[index];
            }
        }
        return sum + delta;
    }
};
#endif //CPP_PRIMER_LEETCODE_122_H


//
// Created by g00522859 on 2020/6/12.
//

#ifndef CPP_PRIMER_LEETCODE_208_H
#define CPP_PRIMER_LEETCODE_208_H
#include <string>
using std::string;

class TrieNode{
public:
    bool isEnd;
    TrieNode* children[26];
    TrieNode() {
        isEnd = false;
        for (int i = 0; i < 26; i++) {
            children[i] = nullptr;
        }
    }
};

class Trie {
private:
    TrieNode* root;
public:
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }

    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* cur = root;
        for (int i = 0; i < word.size(); i++) {
            int index = word[i] - 'a';
            if (cur->children[index] == nullptr) {
                cur->children[index] = new TrieNode();
            }
            cur = cur->children[index];
        }
        cur->isEnd = true;
    }

    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* cur = root;
        for (int i = 0; i < word.size(); i++) {
            int index = word[i] - 'a';
            if (cur->children[index] == nullptr) {
                return false;
            }
            cur = cur->children[index];
        }
        return cur->isEnd;
    }

    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        TrieNode* cur = root;
        for (int i = 0; i < prefix.size(); i++) {
            int index = prefix[i] - 'a';
            if (cur->children[index] == nullptr) {
                return false;
            }
            cur = cur->children[index];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
#endif //CPP_PRIMER_LEETCODE_208_H


//
// Created by g00522859 on 2020/5/25.
//

#ifndef CPP_PRIMER_LEETCODE_503_H
#define CPP_PRIMER_LEETCODE_503_H
#include <vector>
#include <stack>
using std::vector;
using std::stack;

class LeetCode_503 {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        vector<int> result;
        int round = nums.size();
        for (int i = 0; i < nums.size(); i++) {
            int target = nums[i];
            bool found = false;
            for (int j = (i + 1)%round; j != i; j =  (j+1)%round) {
                if (nums[j] > target) {
                    found = true;
                    result.emplace_back(nums[j]);
                    break;
                }
            }
            if (!found) {
                result.emplace_back(-1);
            }
        }
        return result;
    }

    vector<int> nextGreaterElementsBetter(vector<int>& nums) {
        vector<int> doubleNum(nums);
        for (int i = 0; i < nums.size(); i++) doubleNum.emplace_back(nums[i]);
        vector<int> result(nums.size(), -1);
        stack<int> notFound; // save index of not found
        // use i in doubleNum to compare the value before
        for (int i = 0; i < doubleNum.size(); i++) {
            // test stack peek'value and nums[i]
            while (!notFound.empty() && (doubleNum[i] > nums[notFound.top()])) {
                // current value larger than notFound.top, find and pop
                if (notFound.top() < nums.size()) // other values are not interested
                    result[notFound.top()] = doubleNum[i];
                notFound.pop();
            }
            // push index into stack, for next round
            notFound.push(i);
        }
        return result;
    }

};
#endif //CPP_PRIMER_LEETCODE_503_H


//
// Created by g00522859 on 2020/6/5.
//

#ifndef CPP_PRIMER_LEETCODE_739_H
#define CPP_PRIMER_LEETCODE_739_H

#include <vector>
#include <stack>
using std::vector;
using std::stack;
class LeetCode_739 {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        vector<int> result(T.size(), 0);
        stack<int> s;
        for (int i = 0; i < T.size(); i++) {
            while(!s.empty() && T[s.top()] < T[i]) {
                int top = s.top();
                result[top] = i - top;
                s.pop();
            }
            s.push(i);
        }
        return result;
    }
};
#endif //CPP_PRIMER_LEETCODE_739_H


//
// Created by g00522859 on 2020/6/9.
//

#ifndef CPP_PRIMER_LEETCODE_820_H
#define CPP_PRIMER_LEETCODE_820_H
#include <string>
#include <vector>
#include <algorithm>
#include "Trie.h"

using namespace std;

class LeetCode_820 {
public:
//    bool cover(string &a, string &b) {
//        int index = a.size() > b.size()? b.size() : a.size();
//        string strShort = a.size() > b.size()? b : a;
//        string strLong = a.size() > b.size()? a : b;
//        int diff = strLong.size() - strShort.size();
//        for (int i = index -1; i >=0; i--) {
//            if (strLong[diff + i] != strShort[i]) {
//                return false;
//            }
//        }
//        return true;
//    }
//
//    int minimumLengthEncoding(vector<string>& words) {
//        vector<string> result;
//        if (words.size() == 1) {
//            return words[0].size() + 1;
//        }
//        result.emplace_back(words[0]);
//        for (int i = 1; i < words.size(); i++) {
//            bool found = false;
//            for (int j = 0; j < result.size(); j++) {
//                if (cover(words[i], result[j])) {
//                    found = true;
//                    if (words[i].size() > result[j].size()) {
//                        result[j] = words[i];
//                    }
//                    break;
//                }
//            }
//            if (!found) {
//                result.emplace_back(words[i]);
//            }
//        }
//        int count = 0;
//        for(auto i : result) {
//            count += i.size() + 1;
//        }
//        return count;
//    }

    int minimumLengthEncoding(vector<string>& words) {
        Trie trie = Trie();
        int count = 0;
        for (int i = 0; i < words.size(); i++) {
            reverse(words[i].begin(), words[i].end());
        }

        sort(words.begin(), words.end());
        reverse(words.begin(), words.end());

        for (int i = 0; i < words.size(); i++) {
            int tem = trie.insertNode(words[i]);
            if (tem > 0) count += tem + 1;
        }
        return count;
    }
};

#endif //CPP_PRIMER_LEETCODE_820_H


//
// Created by g00522859 on 2020/6/20.
//

#ifndef CPP_PRIMER_LEETCODE_1094_H
#define CPP_PRIMER_LEETCODE_1094_H
#include <vector>
using std::vector;

class Solution {
public:
    bool carPooling(vector<vector<int>>& trips, int capacity) {
        vector<int> v(1000+2, 0);
        int max = 0;
        for (int i = 0; i < trips.size(); i++) {
            vector<int> item = trips[i];
            int size = item[0];
            int start = item[1];
            int end = item[2];
            v[start] += size;
            v[end] -= size;
            max = max > end ? max : end;
        }
        for (int i = 1; i <= max; i ++) {
            v[i] += v[i - 1];
            if (v[i] > capacity) return false;
        }
        return true;
    }
};

#endif //CPP_PRIMER_LEETCODE_1094_H
