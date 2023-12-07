# smallest to biggest:

O(1)
O(log(n))
O(sqrt(n))
O(n)
O(nlog(n))
O(n^2)
O(n^3)
O(2^n)
O(c^n)
O(n!)

# O(1)

Constant Time.
All of these operations work in constant time.
Removing from the end of an array is constant.

```python
# Arrays
nums = [1, 2, 3]
nums.append(4) # addition to end
nums.pop() # remove from end
nums[0] # lookup

# HashMap / Set
hash_map = {}
hash_map["a"] = 10 # insert
"key" in hash_map # lookup
hash_map["key"] # lookup
hash_map.pop("key") # remove
```

# O(n)

Linear Growth.
Standard looping increases as the list increases.
Inserting or removing in an arbitrary position of an array, means you may have to go all the way to the end. Or has to move all items in the array.
Searching an array, means you have to look at EVERY element in an array.

```python
nums = [1, 2, 3] # sum the array, it is looping
for n in nums: # looping
    print(n)

nums.insert(1, 100) # insert middle
nums.remove(100) # remove from middle
100 in nums # search

import heapq
heapq.heapify(nums) # build heap
```

Some nested loops can be O(n) ie: monotonic stack or sliding window.

Monotonic:
https://leetcode.com/problems/daily-temperatures/description/

Sliding Window:
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

# O(n^2)

Nested loops to loop over sets of arrays.
A grid, or pairing elements of an individual array.
Insertion sort (insert in middle n times -> n^2)

```python
# Traverse a square grid
nums = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
for i in range(len(nums)):
    for j in range(len(nums[i])):
        print(nums[i][j])


# Get every pair of elements in array
nums = [1, 2, 3]
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        print(nums[i], nums[j])

# Insertion sort (insert in middle n times -> n^2)
```

# O(n \* m)

A two dimensional matrix that may not be a square.

```python
# Get every pair of elements from two arrays
nums1, nums2 = [1, 2, 3], [4, 5]
for i in range(len(nums1)):
    for j in range(len(nums2)):
        print(nums1[i], nums2[j])

# Traverse rectangle grid
nums = [[1, 2, 3], [4, 5, 6]]
for i in range(len(nums)):
    for j in range(len(nums[i])):
        print(nums[i][j])
O( n^3 )
# Get every triplet of elements in array
nums = [1, 2, 3]
for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        for k in range(j + 1, len(nums)):
            print(nums[i], nums[j], nums[k])

```

# O(log(n))

Used with Binary Search on an array or on a Binary Search Tree
Pushing and popping from a Heap.

On an array, binary search runs in log(n) because on every iteration of the loop, we remove half of the elements. We keep cutting the array until nothing is remaining.

- Given a value of n, how many times can you divide it by 2
- Another way to describe this is given 1 \* 2, how many times do you multiple this by 2 until it equals n. So, 2 to the power
  2^x = n
  log (2^x) = log (n)
  x = log(n)
  The number of times you can divide an array by 2 is log(n)

With a balanced binary search tree, you keep splitting half of the tree over and over.

log(n) grows really slowly. It is practically a flat line.
Inputs of billions still results in 32.

```python
# Binary search
nums = [1, 2, 3, 4, 5]
target = 6
l, r = 0, len(nums) - 1
while l <= r:
    m = (l + r) // 2
    if target < nums[m]:
        r = m - 1
    elif target > nums[m]:
        l = m + 1
    else:
        print(m)
        break

# Binary Search on BST
def search(root, target):
    if not root:
        return False
    if target < root.val:
        return search(root.left, target)
    elif target > root.val:
        return search(root.right, target)
    else:
        return True

# Heap Push and Pop
import heapq
minHeap = []
heapq.heappush(minHeap, 5)
heapq.heappop(minHeap)
```

# O(nlog(n))

Common algos include:

- MergeSort
- assume built in sorting is is nlog(n)
- HeapSort

Popping from a heap is O(log(n))
If we keep popping from a Heap until it is empty, we are adding O(n)

```python
# HeapSort
import heapq
nums = [1, 2, 3, 4, 5]
heapq.heapify(nums)     # O(n)
while nums:
    heapq.heappop(nums) # O(logn)

# MergeSort (and most built-in sorting functions)
```

# O(2^n)

Non polynomial.

- Have this with recursion.
- Computing fibonacci

```python
# Recursion, tree height n, two branches
def recursion(i, nums):
    if i == len(nums):
        return 0
    branch1 = recursion(i + 1, nums)
    branch2 = recursion(i + 2, nums)

```

# O(c^n)

Non polynomial.

- the larger base value, more increased runtime complexity.
- when there is an arbitrary number of branches to do recursion on

```python
# c branches, where c is sometimes n.
def recursion(i, nums, c):
    if i == len(nums):
        return 0

    for j in range(i, i + c):
        branch = recursion(j + 1, nums)

```

# O(n!) (n factorial)

- pretty rare
- in permutations
- traveling salesman problem
- extremely inefficient

the factorial: 5! = 5*4*3*2*1
vs exponential: 2^5 = 2*2*2*2*2
we can see that the factorial will grow much quicker

```python
# Get all factors of n
import math
n = 12
factors = set()
for i in range(1, int(math.sqrt(n)) + 1):
    if n % i == 0:
        factors.add(i)
        factors.add(n // i)
#O( n! )
# Permutations
# Travelling Salesman Problem
```

# O(sqrt(n))

- unused typically
- get all factors of a value
- go through all values from 1 to n

```python
import math
n = 12
factors = set()
for i in range(1, int(math.sqrt(n)) + 1):
    if n % i == 0:
        factors.add(i)
        factors.add(n // i)
print(factors)
```
