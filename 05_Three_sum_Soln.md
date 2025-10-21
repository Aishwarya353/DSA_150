https://leetcode.com/problems/3sum/

https://neetcode.io/problems/three-integer-sum?list=neetcode150


 **Description**
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] where nums[i] + nums[j] + nums[k] == 0, and the indices i, j and k are all distinct.

The output should not contain any duplicate triplets. You may return the output and the triplets in any order.

Example 1:

Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]
Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].

Example 2:

Input: nums = [0,1,1]

Output: []
Explanation: The only possible triplet does not sum up to 0.

Example 3:

Input: nums = [0,0,0]

Output: [[0,0,0]]

Explanation: The only possible triplet sums up to 0.

Constraints:

3 <= nums.length <= 1000
-10^5 <= nums[i] <= 10^5


----

Pattern : Two Pointer Approach

----

**Brute in C#**

    public class Solution {
        public List<List<int>> ThreeSum(int[] nums) {
            var result = new HashSet<string>();
            var resultReturned = new List<List<int>>();
            for(int i = 0; i<=nums.Length-1; i++)
            {
                for(int j = i+1; j<=nums.Length-1; j++)
                {
                    for(int k = j+1; k<=nums.Length-1; k++)
                    {
                        if(nums[i]+nums[j]+nums[k]==0)
                        {
                            List<int> temp = new List<int>(){nums[i],nums[j],nums[k]};
                            var sorted = temp.OrderBy(x=>x).ToList();
                            var st = string.Join(',',sorted);
                            if(!result.Contains(st))
                            {
                                result.Add(st);
                                resultReturned.Add(sorted);
                            }
                        }
                    }
                }
            }
            return resultReturned;
        }
    }

**Brute in Python**

    class Solution:
        def threeSum(self, nums: List[int]) -> List[List[int]]:
            result = set()
            for i in range(len(nums)):
                for j in range(i+1,len(nums)):
                    for k in range(j+1,len(nums)):
                        if nums[i]+nums[j]+nums[k] == 0:
                            #triplet = sorted([nums[i],nums[j],nums[k]])
                            #TypeError: unhashable type: 'list'so the below code
                            triplet = tuple(sorted((nums[i],nums[j],nums[k])))
                            result.add(triplet)
            return [list(l) for l in result]


**Better in C# for generic List**

    public class Solution {
        public List<List<int>> ThreeSum(int[] nums) {
            var result = new HashSet<string>();
            var resultReturned = new List<List<int>>();
            Dictionary<int,int> dict = new Dictionary<int,int>();
            for(int i = 0; i<=nums.Length-1; i++)
            {
                var tempo = new HashSet<int>();
                int target = -nums[i];
                for(int j=i+1; j<=nums.Length-1; j++)
                {
                    int compliment = target - nums[j];
                    if(tempo.Contains(compliment))
                    {
                        var temp = new List<int>() {nums[i],nums[j],compliment};
                        var sorted = temp.OrderBy(x=>x).ToList();
                        var st = string.Join(",",sorted);
                        if(!result.Contains(st))
                        {
                            result.Add(st);
                            resultReturned.Add(sorted);
                        }
                    }
                    else
                    {
                        tempo.Add(nums[j]);
                    }
                }
            }
            return resultReturned;
        }
    }

  **Better in C# for non generic list**
  
      public class Solution {
        public IList<IList<int>> ThreeSum(int[] nums) {
            var result = new HashSet<string>();
            var resultReturned = new List<IList<int>>();
            for(int i = 0; i<=nums.Length-1; i++)
            {
                var tempo = new HashSet<int>();
                int target = -nums[i];
                for(int j=i+1; j<=nums.Length-1; j++)
                {
                    int compliment = target - nums[j];
                    if(tempo.Contains(compliment))
                    {
                        var temp = new List<int>() {nums[i],nums[j],compliment};
                        var sorted = temp.OrderBy(x=>x).ToList();
                        var st = string.Join(",",sorted);
                        if(!result.Contains(st))
                        {
                            result.Add(st);
                            resultReturned.Add(sorted);
                        }
                    }
                    else
                    {
                        tempo.Add(nums[j]);
                    }
                }
            }
            return resultReturned;
    
        }
    }

**Better in Python**
