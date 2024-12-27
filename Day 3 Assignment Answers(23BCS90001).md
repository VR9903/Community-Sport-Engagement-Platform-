#  Function & Recursion DSA Questions

## 1. Fibonacci Series Using Recursion

### Ans:- 

```cpp
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n == 0) {
        return 0;
    } else if (n == 1) {
        return 1;
    } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}

int main() {
    int n;
    cout << "Enter a number (0 <= n <= 30): ";
    cin >> n;

    if (n < 0 || n > 30) {
        cout << "Please enter a number within the range 0 to 30." << endl;
        return 1;
    }

    cout << "F(" << n << ") = " << fibonacci(n) << endl;

    return 0;
}
```

## 2. Reverse Linked List

### Ans:- 

```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseListIterative(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr) {
        ListNode* nextTemp = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextTemp;
    }
    return prev;
}

ListNode* reverseListRecursive(ListNode* head) {
    if (!head || !head->next) {
        return head;
    }
    ListNode* newHead = reverseListRecursive(head->next);
    head->next->next = head;
    head->next = nullptr;
    return newHead;
}

void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    cout << "Original List: ";
    printList(head);

    ListNode* reversedHeadIterative = reverseListIterative(head);
    cout << "Reversed List (Iterative): ";
    printList(reversedHeadIterative);

    ListNode* head2 = new ListNode(1);
    head2->next = new ListNode(2);
    cout << "Reversed List (Recursive): ";
    ListNode* reversedHeadRecursive = reverseListRecursive(head2);
    printList(reversedHeadRecursive);

    return 0;
}
```

## 3. Add Two Numbers

### Ans:-

```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode* dummyHead = new ListNode(0);
    ListNode* current = dummyHead;
    int carry = 0;

    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) {
            sum += l1->val;
            l1 = l1->next;
        }
        if (l2) {
            sum += l2->val;
            l2 = l2->next;
        }
        carry = sum / 10;
        current->next = new ListNode(sum % 10);
        current = current->next;
    }
    return dummyHead->next;
}

void printList(ListNode* head) {
    while (head) {
        cout << head->val << " ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    ListNode* l1 = new ListNode(2);
    l1->next = new ListNode(4);
    l1->next->next = new ListNode(3);

    ListNode* l2 = new ListNode(5);
    l2->next = new ListNode(6);
    l2->next->next = new ListNode(4);

    ListNode* result = addTwoNumbers(l1, l2);
    cout << "Output: ";
    printList(result);

    return 0;
}
```

## 4. Wild Card Matching

### Ans:- 

```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isMatch(string s, string p) {
    int sLen = s.length(), pLen = p.length();
    vector<vector<bool>> dp(sLen + 1, vector<bool>(pLen + 1, false));
    dp[0][0] = true;

    for (int j = 1; j <= pLen; j++) {
        if (p[j - 1] == '*') {
            dp[0][j] = dp[0][j - 1];
        }
    }

    for (int i = 1; i <= sLen; i++) {
        for (int j = 1; j <= pLen; j++) {
            if (p[j - 1] == s[i - 1] || p[j - 1] == '?') {
                dp[i][j] = dp[i - 1][j - 1];
            } else if (p[j - 1] == '*') {
                dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
            }
        }
    }
    return dp[sLen][pLen];
}

int main() {
    string s = "aa";
    string p = "*";
    cout << (isMatch(s, p) ? "true" : "false") << endl;

    s = "aa";
    p = "a";
    cout << (isMatch(s, p) ? "true" : "false") << endl;

    s = "cb";
    p = "?a";
    cout << (isMatch(s, p) ? "true" : "false") << endl;

    return 0;
}
```

## 5. Special Binary String

### Ans:-

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

string makeLargestSpecial(string s) {
    int count = 0, last = 0;
    vector<string> special;

    for (int i = 0; i < s.length(); i++) {
        count += (s[i] == '1') ? 1 : -1;
        if (count == 0) {
            special.push_back("1" + makeLargestSpecial(s.substr(last + 1, i - last - 1)) + "0");
            last = i + 1;
        }
    }
    sort(special.rbegin(), special.rend());
    string result;
    for (const string& str : special) {
        result += str;
    }
    return result;
}

int main() {
    string s1 = "11011000";
    cout << makeLargestSpecial(s1) << endl;

    string s2 = "10";
    cout << makeLargestSpecial(s2) << endl;

    return 0;
}
```

## 6. Write a Function to Print First Name and Last Name

### Ans:-

```cpp
#include <iostream>
#include <string>
using namespace std;

void print_full_name(string first, string last) {
    cout << "Hello " << first << " " << last << "! You just delved into using the function." << endl;
}

int main() {
    string first, last;
    getline(cin, first);
    getline(cin, last);
    print_full_name(first, last);
    return 0;
}
```

## 7. Find GCD of Number Using Function

### Ans:-

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int findGCD(vector<int>& nums) {
    int minNum = *min_element(nums.begin(), nums.end());
    int maxNum = *max_element(nums.begin(), nums.end());
    return gcd(minNum, maxNum);
}

int main() {
    vector<int> nums = {2, 5, 6, 9, 10};
    cout << findGCD(nums) << endl;

    nums = {7, 5, 6, 8, 3};
    cout << findGCD(nums) << endl;

    nums = {3, 3};
    cout << findGCD(nums) << endl;

    return 0;
}
```

## 8. Longest Substring Without Repeating Characters

### Ans:-

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int findGCD(vector<int>& nums) {
    int minNum = *min_element(nums.begin(), nums.end());
    int maxNum = *max_element(nums.begin(), nums.end());
    return gcd(minNum, maxNum);
}

int main() {
    vector<int> nums = {2, 5, 6, 9, 10};
    cout << findGCD(nums) << endl;

    nums = {7, 5, 6, 8, 3};
    cout << findGCD(nums) << endl;

    nums = {3, 3};
    cout << findGCD(nums) << endl;

    return 0;
}
```

## 9. Maximum Subarray Product

### Ans:-

```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxProduct(vector<int>& nums) {
    int maxProd = nums[0], minProd = nums[0], result = nums[0];

    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] < 0) {
            swap(maxProd, minProd);
        }
        maxProd = max(nums[i], maxProd * nums[i]);
        minProd = min(nums[i], minProd * nums[i]);
        result = max(result, maxProd);
    }
    return result;
}

int main() {
    vector<int> nums = {2, 3, -2, 4};
    cout << maxProduct(nums) << endl;

    nums = {-2, 0, -1};
    cout << maxProduct(nums) << endl;

    nums = {3, -1, 4};
    cout << maxProduct(nums) << endl;

    return 0;
}
```

## 10. There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

### Ans:-

```cpp
#include <iostream>
#include <vector>
using namespace std;

int candy(vector<int>& ratings) {
    int n = ratings.size();
    vector<int> candies(n, 1);

    for (int i = 1; i < n; i++) {
        if (ratings[i] > ratings[i - 1]) {
            candies[i] = candies[i - 1] + 1;
        }
    }

    for (int i = n - 2; i >= 0; i--) {
        if (ratings[i] > ratings[i + 1]) {
            candies[i] = max(candies[i], candies[i + 1] + 1);
        }
    }

    int totalCandies = 0;
    for (int candy : candies) {
        totalCandies += candy;
    }
    return totalCandies;
}

int main() {
    vector<int> ratings1 = {1, 0, 2};
    cout << candy(ratings1) << endl;

    vector<int> ratings2 = {1, 2, 2};
    cout << candy(ratings2) << endl;

    return 0;
}
```

