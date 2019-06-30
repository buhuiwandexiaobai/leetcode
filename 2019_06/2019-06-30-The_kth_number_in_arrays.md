#### 题目：找出数组中第k大的数字。

#### 思路：最简单的方法就是讲数组降序排序，数组第k个元素便是第k大的数字。冒泡排序也可以，冒k次泡即可，这里使用快速排序，每次将数组一份为二的时候可以比较二分的位置和k的大小，相等则就找到第k大的元素，如果比k小的话，则在右边递归查找，反之在左半部分查找。

代码：
```
class Solution {
    public int findKthLargest (int[] nums, int k) {
        k = k - 1;
        int left = 0, right = nums.length - 1;
        while (left < right) {
            int index = partition(nums, left, right);
            if (index < k) {
                left = index +1;
            } else if (index > k) {
                right = index - 1;
            } else {
                break;
            }
        }
        return nums[k];
    }
    
    private int partition (int[] nums, int left, int right) {
        int val = nums[left];
        while (left < right) {
            while (left < right && nums[right] < val) {
                right--;
            }
            nums[left] = nums[right];
            while (left < right && nums[left] >= val) {
                left++;
            }
            nums[right] = nums[left];
        }
        nums[left] = val;
        return left;
    }
}
```
