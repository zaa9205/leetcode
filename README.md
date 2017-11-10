# 229. Majority Element II (Medium)

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.   

## Round 1

![Alt Text](https://raw.githubusercontent.com/zaa9205/images/master/229.Majority%20Element%20II.png)

```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
        int flag1 = 999999;
        int flag2 = 889988;
        int count1 = 0;
        int count2 = 0;
        
        // cannot change the sequence of if conditions, becuase we need to determine the num is in flag or not, if num == flag1 and flag2 count is empty, in this situation the num should be add to flag1 count, not flag2 = num, count2++
        for (int num : nums) {
            if (num == flag1) {
                count1++;
            } else if (num == flag2) {
                count2++;
            } else if (count1 == 0) {
                flag1 = num;
                count1++;
            } else if (count2 == 0) {
                flag2 = num;
                count2++;
            } else if (num != flag1 && num != flag2) {
                count1--;
                count2--;
            }
        }
        
        count1 = 0;
        count2 = 0;
        
        for (int num : nums) {
            if (num == flag1) {
                count1++;
            } else if (num == flag2) {
                count2++;
            }
        }
        
        //determine the majority elements are exist or not.
        List<Integer> res = new ArrayList<>();
        if (count1 > nums.length / 3) {
            res.add(flag1);
        }
        if (count2 > nums.length / 3) {
            res.add(flag2);
        }
        
        return res;
    }
}
```
