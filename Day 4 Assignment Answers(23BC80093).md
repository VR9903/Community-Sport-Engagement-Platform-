# Answers
## Q1.MinStack

```python
class MinStack:
  def __init__(self):
    self.stack = []
    self.min_stack = []

  def push(self, val: int) -> None:
    self.stack.append(val)
    if not self.min_stack or val <= self.min_stack[-1]:
      self.min_stack.append(val)

  def pop(self) -> None:
    if self.stack:
      popped = self.stack.pop()
      if popped == self.min_stack[-1]:
        self.min_stack.pop()

  def top(self) -> int:
    if self.stack:
      return self.stack[-1]
    return None

  def getMin(self) -> int:
    if self.min_stack:
      return self.min_stack[-1]
    return None
```
## Q2.Number of Students Unable to Eat Lunch
```python
from collections import deque

def students_unable_to_eat(students, sandwiches):
  student_queue = deque(students)
  sandwich_stack = deque(sandwiches)
  count = 0

  while student_queue and sandwich_stack:
    current_student = student_queue.popleft()
    current_sandwich = sandwich_stack[0]

    if current_student == current_sandwich:
      sandwich_stack.popleft()
    else:
      student_queue.append(current_student)
      count += 1

      # Check for loop (all students have been to the end of the queue)
      if len(student_queue) == len(students) and student_queue == deque(students):
        break
```
## Q3.Next Greater Element II
```python
from collections import deque

def next_greater_element(nums):
  n = len(nums)
  result = [-1] * n
  stack = deque()

  for i in range(2 * n - 1, -1, -1):
    current = nums[i % n]

    # Pop elements smaller than current and update their next greater element
    while stack and stack[-1] < current:
      result[stack.pop()] = current
    stack.append(i % n)

  return result
  return count
```
## Q4.Sliding Window Maximum
```python
from collections import deque

def sliding_window_maximum(nums, k):
  result = []
  window = deque()

  for i, num in enumerate(nums):
    # Add element to window
    window.append(num)
```
## Q5.Poisonous plants
``` python
def poisonousPlants(p):
    n = len(p)
    if n <= 1:
        return 0

    days = 0
    plants = p[:]  # Create a copy to avoid modifying the original list

    while True:
        died = []
        for i in range(1, len(plants)):
            if plants[i] > plants[i - 1]:
                died.append(i)

        if not died:
            break

        days += 1
        new_plants = []
        for i in range(len(plants)):
            if i not in died:
                new_plants.append(plants[i])
        plants = new_plants

    return days
```

