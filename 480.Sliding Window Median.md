# Sliding Window Median (Hard)

**Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.**

**Examples: 
[2,3,4] , the median is 3**

**[2,3], the median is (2 + 3) / 2 = 2.5**

**Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Your job is to output the median array for each window in the original array.**

**For example,
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.**

**Window position                Median**

**[1  3  -1] -3  5  3  6  7       1**

**1 [3  -1  -3] 5  3  6  7       -1**

**1  3 [-1  -3  5] 3  6  7       -1**

**1  3  -1 [-3  5  3] 6  7       3**

**1  3  -1  -3 [5  3  6] 7       5**

**1  3  -1  -3  5 [3  6  7]      6**

**Therefore, return the median sliding window as [1,-1,-1,3,5,6].**

```java
class Solution {
    
    PriorityQueue<Integer> min = new PriorityQueue<>((o1, o2) -> o1 == o2 ? 0 : o1 > o2 ? -1 : 1);
    PriorityQueue<Integer> max = new PriorityQueue<>((o1, o2) -> o1 == o2 ? 0 : o1 > o2 ? 1 : -1);
    
    public double[] medianSlidingWindow(int[] nums, int k) {
        int len = nums.length;
        double[] ans = new double[len - k + 1];
        
        for (int i = 0; i < len; i ++) {
            add_num(nums[i]);
            
            if (i - k >= 0)
                remove_overflow(nums[i - k]);
            
            if (i - k + 1 >= 0)
                ans[i - k + 1] = get_median();
        }
        
        return ans;
    }
    
    private void add_num(int num) {
        if (min.isEmpty() || num < min.peek())
            min.add(num);
        else max.add(num);
        
        if (min.size() > max.size() + 1)
            max.add(min.poll());
        if (max.size() > min.size())
            min.add(max.poll());
    }
    
    private void remove_overflow(int overflow) {
        if (overflow <= min.peek())
            min.remove(overflow);
        else max.remove(overflow);
        
        if (min.size() > max.size() + 1)
            max.add(min.poll());
        if (max.size() > min.size())
            min.add(max.poll());
    }
    
    private double get_median() {
        if (min.size() == max.size())
            return ((double)min.peek() + (double)max.peek()) / 2.0;
        else return (double)min.peek();
    }
}
```
