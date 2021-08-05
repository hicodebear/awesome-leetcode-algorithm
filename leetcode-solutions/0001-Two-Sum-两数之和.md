<p align="center">
  <a href="https://mp.weixin.qq.com/s/TsTcCDboXwnTnUeIW3Zg9Q"><img src="https://img.shields.io/badge/LeetCode组队刷题群-blueviolet" alt=""></a>
</p>

## 0001-Two-Sum-两数之和
https://leetcode-cn.com/problems/two-sum/

## 题意

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**样例**

```txt
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```


## 题解

哈希可以快速查找一个数字。

建立哈希表，key等于数组的值，value等于值所对应的下标。

然后遍历数组，每次遍历到位置`i`时，检查 `target-num[i]` 是否存在，注意`target-num[i]`的位置不能等于`i`。

下图以示例演示一下哈希表，将数组插入到哈希表中，查找给定的`key`，即可以在`O(1)` 的时间复杂度查找到，图中的a、b、c、d指的是哈希表的索引。

<img width="476" alt="示例" src="https://user-images.githubusercontent.com/87517460/128287010-e268ab24-d3fd-495e-ad8c-16703ad4251e.png">


## Java代码

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> numExist = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; ++i) {
            if (numExist.containsKey(target - nums[i])) {
                return new int[]{i, numExist.get(target - nums[i])};
            }
            numExist.put(nums[i], i);
        }
        return new int[2];
    }
}
```

## C++代码

```c++
class Solution {
public:
    unordered_map<int, int> numExist;
    vector<int> twoSum(vector<int> &nums, int target) {
      vector<int> ans;
      for (int i = 0; i < nums.size(); i++) {
        int b = target - nums[i];
        if (numExist.count(b)) {
          ans.push_back(i);
          ans.push_back(numExist.at(b));
          break;
        }
        numExist[nums[i]] = i;
      }
      return ans;
    }
};
```
