
2024-08-29 14:05

Status: finished, memorized: for now
Memorization check: y, x, x, x, x, x, x, x, x, x,

Tags: [[Set]], [[For statement loop]], [[LeetCode]]

# Kth Distinct String in Array


A **distinct string** is a string that is present only **once** in an array.

Given an array of strings `arr`, and an integer `k`, return _the_ `kth` _**distinct string** present in_ `arr`. If there are **fewer** than `k` distinct strings, return _an **empty string**_ `""`.

Note that the strings are considered in the **order in which they appear** in the array.


solution:










create two sets to keep track of unique elements
iterate over array, add elements to unique set
if element already exists in unique, then add it to not unique
keep iterating if item in not_unique skip etc.

after all elements have been iterated through, 
iterate through array again, find the kth unique one
if i is in unique set, decrement k by 1
once k == 0 and i in unique, return i
else return ""


unique = set()
not_unique = set()
        for i in arr:
            if i in not_unique:
                continue
            if i in unique:
                unique.remove(i)
                not_unique.add(i)
            else:
                unique.add(i)
        for i in arr:
            if i in unique:
                k -= 1
            if k == 0:
                return i
        return ""