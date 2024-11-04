Memorized: yes
https://leetcode.com/problems/contains-duplicate/description/
[[Set]], [[For statement loop]]

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

solution







initialize a set since a set cannot hold duplicates.
iterate through arr,
if arr[i] is in set,
return False

if no duplicates are found return true

myset = set()

  

        for i in range(len(nums)):

            if nums[i] in myset:

                return True

            myset.add(nums[i])

        return False