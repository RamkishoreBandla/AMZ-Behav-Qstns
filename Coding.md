🔹 1. Two Sum (Array + Hash Map)
Q: Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

✅ Python Solution:
python
Copy
Edit
def twoSum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        diff = target - num
        if diff in seen:
            return [seen[diff], i]
        seen[num] = i
📌 Time Complexity: O(n)
📌 Space: O(n)
📌 Amazon Tip: They may ask a follow-up: what if the array is sorted? Then use two pointers.

🔹 2. Longest Substring Without Repeating Characters (Sliding Window)
Q: Given a string s, find the length of the longest substring without repeating characters.

✅ Python Solution:
python
Copy
Edit
def lengthOfLongestSubstring(s):
    char_set = set()
    left = max_len = 0
    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        max_len = max(max_len, right - left + 1)
    return max_len
📌 Time Complexity: O(n)
📌 Amazon Tip: Sliding window technique is a favorite. Understand variations like at most K distinct characters.

🔹 3. Merge Intervals
Q: Given an array of intervals, merge all overlapping intervals.

✅ Python Solution:
python
Copy
Edit
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = []
    for interval in intervals:
        if not merged or merged[-1][1] < interval[0]:
            merged.append(interval)
        else:
            merged[-1][1] = max(merged[-1][1], interval[1])
    return merged
📌 Time Complexity: O(n log n)
📌 Amazon Tip: Sorting first helps avoid quadratic complexity.

🔹 4. Top K Frequent Elements (Heap + Hash Map)
Q: Given an integer array nums and an integer k, return the k most frequent elements.

✅ Python Solution:
python
Copy
Edit
from collections import Counter
import heapq

def topKFrequent(nums, k):
    count = Counter(nums)
    return [item for item, _ in heapq.nlargest(k, count.items(), key=lambda x: x[1])]
📌 Time Complexity: O(n log k)
📌 Space: O(n)
📌 Amazon Tip: Also practice variations using bucket sort for linear time.

🔹 5. Valid Parentheses (Stack)
Q: Given a string containing '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

✅ Python Solution:
python
Copy
Edit
def isValid(s):
    stack = []
    mapping = {')': '(', ']': '[', '}': '{'}
    for char in s:
        if char in mapping:
            top = stack.pop() if stack else '#'
            if mapping[char] != top:
                return False
        else:
            stack.append(char)
    return not stack
📌 Time Complexity: O(n)
📌 Amazon Tip: Questions around balanced parentheses are frequent in SDE I/II rounds.

🔹 6. Find the Median of Two Sorted Arrays (Binary Search)
Q: Hard-level: Find the median of two sorted arrays in O(log(min(n, m))) time.

✅ Python Solution:
python
Copy
Edit
def findMedianSortedArrays(nums1, nums2):
    A, B = nums1, nums2
    if len(A) > len(B):
        A, B = B, A
    total = len(A) + len(B)
    half = total // 2

    l, r = 0, len(A) - 1
    while True:
        i = (l + r) // 2
        j = half - i - 2

        Aleft = A[i] if i >= 0 else float('-infinity')
        Aright = A[i+1] if (i+1) < len(A) else float('infinity')
        Bleft = B[j] if j >= 0 else float('-infinity')
        Bright = B[j+1] if (j+1) < len(B) else float('infinity')

        if Aleft <= Bright and Bleft <= Aright:
            if total % 2:
                return min(Aright, Bright)
            return (max(Aleft, Bleft) + min(Aright, Bright)) / 2
        elif Aleft > Bright:
            r = i - 1
        else:
            l = i + 1
📌 Amazon Tip: Know how to use binary search on partitions.

🔹 7. Kth Largest Element in an Array (Min-Heap)
Q: Find the kth largest element in an unsorted array.

✅ Python Solution:
python
Copy
Edit
import heapq

def findKthLargest(nums, k):
    return heapq.nlargest(k, nums)[-1]
📌 Time Complexity: O(n log k)
📌 Amazon Tip: Expect to optimize space if they ask you to do it in-place.

🔹 8. Lowest Common Ancestor (Binary Tree DFS)
Q: Given a binary tree, find the lowest common ancestor (LCA) of two nodes.

✅ Python Solution:
python
Copy
Edit
def lowestCommonAncestor(root, p, q):
    if not root or root == p or root == q:
        return root
    left = lowestCommonAncestor(root.left, p, q)
    right = lowestCommonAncestor(root.right, p, q)
    if left and right:
        return root
    return left or right
📌 Amazon Tip: Know how to traverse binary trees using post-order DFS.

🔹 9. Word Ladder (BFS)
Q: Given two words and a word list, find the shortest transformation sequence from beginWord to endWord.

✅ Python Solution:
python
Copy
Edit
from collections import deque

def ladderLength(beginWord, endWord, wordList):
    wordSet = set(wordList)
    if endWord not in wordSet:
        return 0
    queue = deque([(beginWord, 1)])
    while queue:
        word, steps = queue.popleft()
        if word == endWord:
            return steps
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                nxt = word[:i] + c + word[i+1:]
                if nxt in wordSet:
                    wordSet.remove(nxt)
                    queue.append((nxt, steps + 1))
    return 0
📌 Time Complexity: O(n * 26 * L)
📌 Amazon Tip: They often test graph traversal with word games.

🔹 10. Clone Graph (DFS + Hash Map)
Q: Clone a graph where each node contains a list of its neighbors.

✅ Python Solution:
python
Copy
Edit
def cloneGraph(node):
    if not node:
        return None
    old_to_new = {}

    def dfs(n):
        if n in old_to_new:
            return old_to_new[n]
        copy = Node(n.val)
        old_to_new[n] = copy
        for neighbor in n.neighbors:
            copy.neighbors.append(dfs(neighbor))
        return copy

    return dfs(node)
📌 Amazon Tip: Make sure you understand DFS/BFS traversal with visited maps.
