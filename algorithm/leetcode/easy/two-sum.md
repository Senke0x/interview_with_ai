

第一轮 code
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans = {};
        for (int i = 0; i < nums.size(); i++)
        {
            for (int j = i+1; j < nums.size(); j++)
            {
                if (nums[i] + nums[j] == target)
                {
                    ans = {i,j};
                }
            }
        }
        return ans;
    }
};
```

第二轮 code
- 由于 a+b=target，因此可以通过一次遍历的方式基于一个 map 来记录每个元素的值和索引
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> numMap;
        for (int i = 0; i < nums.size(); i++)
        {
            if (numMap.find(target - nums[i]) != numMap.end())
            {
                return {i, numMap[target - nums[i]]};
            }
            else
            {
                numMap[nums[i]] = i;
            }
        }
        return {0,0};
    }
};
```

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> numsIndex = new HashMap<Integer,Integer>();
        for (int i = 0; i < nums.length; i++)
        {
            if (numsIndex.containsKey(target - nums[i]))
            {
                return new int[]{i, numsIndex.get(target - nums[i])};
            }
            else
            {
                numsIndex.put(nums[i],i);
            }
        }
        return new int[]{0,0};
    }
}
```


