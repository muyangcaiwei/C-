## 搜索旋转排序数组

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 `-1` 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 *O*(log *n*) 级别。

## 思想：

4，5，6，7，*0，1，2，3* 分别为两个递增子序列，并且左子序列均大于右子序列。

二分查找0，

1.当 nums[mid] 等于target时返回index

2.当nums[l] <= nums[mid]时，也就说[l, mid]是在同一个递增序列里，此时如果target在[l, mid]这个左子序列里，即nums[l] <= target(等号一定要有) && target<nums[mid]时，r = mid - 1;否则target在[mid , r]这个右子序列里，即l = mid + 1;

3.当nums[l] > nums[mid]时，说明[l, mid]间有一个断层，如果target在[mid, right] **(该区间为一个递增序列)** 之间，即nums[mid] < target && target <= nums[r]时，l = mid + 1; 否则target在[l, mid]间，即r = mid - 1;




```C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int len = nums.size();
        if(len == 0)
            return -1;
        

        int l = 0, r = len - 1, mid;
        
        while(l <= r)
        {
            mid = l + (r - l) / 2;
            if(nums[mid] == target)
                return mid;
            if(nums[mid] >= nums[l])
            {
                if(nums[l] <= target && nums[mid] > target)
                    r = mid - 1;
                else
                    l = mid + 1;
            }else 
            {
                if(nums[r] >= target && nums[mid] < target)
                    l = mid + 1;
                else
                    r = mid - 1;
            }
        }
        return -1;
    }
};
```