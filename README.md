# First-Missing-Positive
Given an unsorted integer array nums. Return the smallest positive integer that is not present in nums.  You must implement an algorithm that runs in O(n) time and uses O(1) auxiliary space.

class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        n=len(nums)
        nums.append(n+1)
        has1=False
        for i in range(n+1):
            if nums[i]==1: has1=True
            elif nums[i]<=0 or nums[i]>n:
                nums[i]=1
        
        if has1==False: return 1
        bitMask=(1<<17)-1

        for x in nums:
            seen=x & bitMask
            nums[seen]|=(1<<17)

        for i in range(1, n+1):
            if (nums[i]>>17)==0:
                return i
        return n+1
        
