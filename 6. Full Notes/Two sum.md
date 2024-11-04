
[[Maps]]/[[dictionairy code C]]


Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

dic = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if(complement in dic):
                return [dic[complement], i]
            dic[nums[i]] = i