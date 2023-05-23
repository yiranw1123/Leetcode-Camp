二分查找

-何时应该想到二分查找？
有序数组，无重复元素

- 如何判断边界条件应该怎么写
想清楚循环不变量。对于二分查找来说，区间的定义有两种：左闭右闭[left, right]，左闭右开[left, right)。

左闭右闭[left, right]:left == right是成立的，因为左右都为闭合区间。当nums[mid] > target时， left = mid -1
左闭右开[left, right): left永远应该小于right，所以while loop的跳出条件为left< right.

704.二分查找

    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = left + (right-left) // 2           ----->注意index需要是整数
            if nums[mid] == target: return mid
            elif nums[mid] < target: left = mid + 1
            elif nums[mid] > target: right = mid - 1
        return -1
        
        
     public int search(int[] nums, int target) {
        int n = nums.length;
        int left = 0;
        int right = n -1;
        while(left <= right){
            int mid = left + （right - left) /2; -------> 防止溢出
            if(nums[mid] > target){
                right--;
            } else if(nums[mid] < target){
                left++;
            } else if(nums[mid] == target){
                return mid;
            }
        }
        return -1;
    }

27.移除元素
双指针/快慢指针

题目要求原地移除所有值等于target的元素，不应该使用多余的存储空间。用两个指针遍历整个数组，fast指针如果遇到target就跳过。如果fast指针位置上是非target的数，将其赋在slow指针指向的位置，在循环结束时，slow指针的index即是移除所有target后的数组长度。


    def removeElement(self, nums: List[int], val: int) -> int:
        slow, fast = 0,0
        while fast < len(nums):
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow+=1
            fast+=1
        return slow
        
        
    public int removeElement(int[] nums, int val) {
        int fast = 0, slow = 0;
        while(fast < nums.length){
            //如果fast不是value，赋值给slow，将元素前移
            //如果fast是value则跳过
            if(nums[fast] != val){
                //先赋值再前移slow指针，确保 0 ->（slow-1）为保留元素
                nums[slow] = nums[fast];
                slow++;
            }
            fast++;
        }
        return slow;
    }

