# day2

> 文章讲解

## 977. Squares of a Sorted Array

第一个想法：先计算sqrt后排序。

```
class Solution {
    public int[] sortedSquares(int[] nums) {
        int size = nums.length;
        for (int a=0;a<size;a++){
            nums[a]=nums[a]*nums[a];
        }
        int temp = 0;
        for (int i = nums.length - 1; i > 0; i--) { 
            for (int j = 0; j < i; j++) { 
                if (nums[j] > nums[j + 1]) {
                    temp = nums[j];
                    nums[j] = nums[j + 1];
                    nums[j + 1] = temp;
                }
            }
        }
        return nums;
    }
}

```

五百多毫秒，时间太久了

如果使用双指针的话，有一难点想不通：
1.双指针如何解决负数平方后的排序问题，因为顺序不一样。

搞不明白了。。。
看视频！！！

视频解决了两个问题：
1.non-decreasing order is equal to decreasing order//wtf :(
    这样就表示平方后的数组为先大到小，在小到大的顺序
2.使用双指针的本质为可以对数组可以进行两个方向的筛选，而非昨天的严格快慢指针的动作。更加泛化了这个概念

```
class Solution {
    public int[] sortedSquares(int[] nums) {
        int size = nums.length;
        int[] result= new int[size];
        int k = size-1;
        int i=0;
        int j=size -1;
        while (i<=j){
            if (nums[i]*nums[i]>nums[j]*nums[j]){
                result[k]=nums[i]*nums[i];
                k--;
                i++;
            }
            else {
                result[k]=nums[j]*nums[j];
                k--;
                j--;
            }
        }
        return result;
    }
}
```
good dude

## 209. Minimum Size Subarray Sum

暴力解法就算了，无意义

尴尬，除了暴力解法无思路。。。

看视频！！

```
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int left = 0;
        int sum = 0;
        int result = Integer.MAX_VALUE;
        for (int right = 0; right < nums.length; right++) {
            sum += nums[right];
            while (sum >= target) {
                result = Math.min(result, right - left + 1);
                sum -= nums[left++];
            }
        }
        return result == Integer.MAX_VALUE ? 0 : result;
    }
}
```

大致理解了


## 59. Spiral Matrix II

搞不太懂，只能看题解了。。