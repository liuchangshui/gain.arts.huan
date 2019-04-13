# ATRS WEEK01 (0408-0414)
## Algorithm 
### 题目
```
1. Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
	Given nums = [2, 7, 11, 15], target = 9,

	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].
```

### 解法 1
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for(int i=0; i<nums.length; i++){
            int tempInt = nums[i];
            for(int j=i+1; j<nums.length; j++){
                if(target == (tempInt + nums[j])){
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
        }
        return null;
    }
}
```

### 解法 2
```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> hashMap = new HashMap<Integer,Integer>();
        for(int i=0; i<nums.length; i++){
            int tempResult = target - nums[i];
            if(hashMap.containsKey(tempResult)){
                return new int[] {hashMap.get(tempResult),i};
            }
            hashMap.put(nums[i],i);
        }
        return new int[] {0,0};
    }
}
```
