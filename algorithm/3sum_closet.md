### 16. 最接近的三数之和

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。
```C++
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```
思想：固定第一个整数i，分别使用两个指针 j , k 分别指向 i+1和 len-1，然后判断nums[j] + nums[k] + nums[i]与target的大小关系，使用一个minN记录两者的最小值便于进行比较。
```C++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int len = nums.size();
        int result = 0;
        int minN = INT_MAX;
        if(len < 3)
            return result;
        sort(nums.begin(), nums.end());
        for(int i = 0; i < len - 2; i++)
        {
            int j = i + 1;
   			int k = len - 1;
            while(j < k)
            {
                int tmp = nums[j] + nums[k];
                if(abs(nums[i] + tmp - target) < minN)
                {
                    minN = abs(nums[i] + tmp - target);
                    result = nums[i] + tmp;
                }
                if(nums[i] + tmp == target)
                    return target;
                if(nums[i] + tmp < target)
                {
                    j++;
                }else
                {
                    k--;
                }
                
            }
            
        }
        return result;
    }
};
```