# Very Easy - Searching a Number

```python
def search_number(k, arr):
    for i in range(len(arr)):
        if arr[i] == k:
            return i + 1  # 1-based indexing
    return -1
```

# Easy - Minimum Number of Moves to Seat Everyone

```python
def min_moves_to_seat(seats, students):
    seats.sort()
    students.sort()
    moves = 0
    for i in range(len(seats)):
        moves += abs(seats[i] - students[i])
    return moves
```

# Medium - Search in 2D Matrix

```python
def search_2d_matrix(matrix, target):
    if not matrix or not matrix[0]:
        return False

    m = len(matrix)
    n = len(matrix[0])
    left, right = 0, m * n - 1

    while left <= right:
        mid = (left + right) // 2
        row = mid // n
        col = mid % n
        if matrix[row][col] == target:
            return True
        elif matrix[row][col] < target:
            left = mid + 1
        else:
            right = mid - 1

    return False
```

# Hard - Sort Items by Groups Respecting Dependencies

```python
from collections import defaultdict, deque

def sort_items_by_groups(n, m, group, beforeItems):
    item_graph = defaultdict(list)
    group_graph = defaultdict(list)
    item_indegree = [0] * n
    group_indegree = [0] * m
    items_in_group = defaultdict(list)

    for i in range(n):
        items_in_group[group[i]].append(i)

    for i in range(n):
        for before in beforeItems[i]:
            item_graph[before].append(i)
            item_indegree[i] += 1
            if group[i] != -1 and group[before] != -1 and group[i] != group[before]:
                group_graph[group[before]].append(group[i])
                group_indegree[group[i]] += 1
    
    def topological_sort(graph, indegree, items):
        queue = deque([item for item in items if indegree[item] == 0])
        result = []
        while queue:
            node = queue.popleft()
            result.append(node)
            for neighbor in graph[node]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    queue.append(neighbor)
        return result if len(result) == len(items) else []

    sorted_groups = topological_sort(group_graph, group_indegree, range(m))
    if not sorted_groups:
        return []
    
    result = []
    for grp in sorted_groups:
        sorted_items = topological_sort(item_graph, item_indegree, items_in_group[grp])
        if not sorted_items:
            return []
        result.extend(sorted_items)

    return result
```

# Very Hard - Find Minimum in Rotated Sorted Array II

```python
def find_min_rotated_sorted_array_ii(nums):
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2
        if nums[mid] > nums[right]:
            left = mid + 1
        elif nums[mid] < nums[right]:
            right = mid
        elif nums[left] < nums[mid]:
            left = mid + 1
        else:
            right -= 1  # Crucial for handling duplicates correctly
    return nums[left]
```
