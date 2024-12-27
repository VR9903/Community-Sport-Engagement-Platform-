# Array & Linked List

## Question 1: Majority Elements

### Ans:-

```cpp
#include <iostream>
#include <vector>
using namespace std;

int majorityElement(vector<int>& nums) {
    int candidate = nums[0];
    int count = 1;

    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] == candidate) {
            count++;
        } else {
            count--;
            if (count == 0) {
                candidate = nums[i];
                count = 1;
            }
        }
    }

    return candidate;
}

int main() {
    vector<int> nums1 = {3, 2, 3};
    cout << "Majority Element in [3, 2, 3]: " << majorityElement(nums1) << endl;

    vector<int> nums2 = {2, 2, 1, 1, 1, 2, 2};
    cout << "Majority Element in [2, 2, 1, 1, 1, 2, 2]: " << majorityElement(nums2) << endl;

    return 0;
}
```

## Question 2: Pascal's Triangle

### Ans:-

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<vector<int>> generate(int numRows) {
    vector<vector<int>> triangle;

    for (int i = 0; i < numRows; i++) {
        vector<int> row(i + 1, 1);

        for (int j = 1; j < i; j++) {
            row[j] = triangle[i - 1][j - 1] + triangle[i - 1][j];
        }

        triangle.push_back(row);
    }

    return triangle;
}

int main() {
    int numRows;
    cout << "Enter the number of rows for Pascal's Triangle: ";
    cin >> numRows;

    vector<vector<int>> pascalTriangle = generate(numRows);

    cout << "[";
    for (int i = 0; i < pascalTriangle.size(); i++) {
        cout << "[";
        for (int j = 0; j < pascalTriangle[i].size(); j++) {
            cout << pascalTriangle[i][j];
            if (j < pascalTriangle[i].size() - 1) {
                cout << ",";
            }
        }
        cout << "]";
        if (i < pascalTriangle.size() - 1) {
            cout << ",";
        }
    }
    cout << "]" << endl;

    return 0;
}
```

## Question 3: Container With Most Water

### Ans:-

```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxArea(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int maxArea = 0;

    while (left < right) {
        int width = right - left;
        int currentHeight = min(height[left], height[right]);
        maxArea = max(maxArea, width * currentHeight);
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }

    return maxArea;
}

int main() {
    vector<int> height1 = {1, 8, 6, 2, 5, 4, 8, 3, 7};
    cout << "Max area for height [1, 8, 6, 2, 5, 4, 8, 3, 7]: " << maxArea(height1) << endl;

    vector<int> height2 = {1, 1};
    cout << "Max area for height [1, 1]: " << maxArea(height2) << endl;

    return 0;
}
```

## Question 4: Maximum Number of Groups Getting Fresh Donuts

### Ans:-

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int maxHappyGroups(int batchSize, vector<int>& groups) {
    vector<int> count(batchSize, 0);
    for (int g : groups) {
        count[g % batchSize]++;
    }
    
    int happyGroups = min(count[0], 1);
    count[0] -= happyGroups;
    
    for (int i = 1; i < batchSize; i++) {
        if (count[i] > 0) {
            happyGroups += count[i];
            count[0] -= min(count[i], count[0]);
        }
    }
    
    return happyGroups + (count[0] > 0 ? 1 : 0);
}

int main() {
    int batchSize1 = 3;
    vector<int> groups1 = {1, 2, 3, 4, 5, 6};
    cout << "Max happy groups for batchSize 3: " << maxHappyGroups(batchSize1, groups1) << endl;

    int batchSize2 = 4;
    vector<int> groups2 = {1, 3, 2, 5, 2, 2, 1, 6};
    cout << "Max happy groups for batchSize 4: " << maxHappyGroups(batchSize2, groups2) << endl;

    return 0;
}
```

## Question 5: Find Minimum Time to Finish All Jobs

### Ans:-

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
#include <numeric>
using namespace std;

bool distribute(const vector<int>& jobs, int index, vector<int>& workerTime, int maxTime);

bool canDistribute(const vector<int>& jobs, int k, int maxTime) {
    vector<int> workerTime(k, 0);
    return distribute(jobs, 0, workerTime, maxTime);
}

bool distribute(const vector<int>& jobs, int index, vector<int>& workerTime, int maxTime) {
    if (index == jobs.size()) {
        return true;
    }
    for (int i = 0; i < workerTime.size(); i++) {
        if (workerTime[i] + jobs[index] <= maxTime) {
            workerTime[i] += jobs[index];
            if (distribute(jobs, index + 1, workerTime, maxTime)) {
                return true;
            }
            workerTime[i] -= jobs[index];
        }
        if (workerTime[i] == 0) {
            break;
        }
    }
    return false;
}

int minimumTimeRequired(vector<int>& jobs, int k) {
    int left = *max_element(jobs.begin(), jobs.end());
    int right = accumulate(jobs.begin(), jobs.end(), 0);
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (canDistribute(jobs, k, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}

int main() {
    vector<int> jobs1 = {3, 2, 3};
    int k1 = 3;
    cout << "Minimum time for jobs [3, 2, 3] with 3 workers: " << minimumTimeRequired(jobs1, k1) << endl;

    vector<int> jobs2 = {1, 2, 4, 7, 8};
    int k2 = 2;
    cout << "Minimum time for jobs [1, 2, 4, 7, 8] with 2 workers: " << minimumTimeRequired(jobs2, k2) << endl;

    return 0;
}
```
