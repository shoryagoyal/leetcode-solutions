# Two Sum

### Approach 1 - Using two nested loops

`Explanation`

The brute force approach is to consider all the pairs in the array. We use nested loop to iterate on all the pairs of the array. Now, for each pair of the array we check whether the sum of the pair is equal to the target and as soon as we find such a pair with a sum equal to the target, we update the answer array and break out of the loop.

`Code`

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int ans[] = new int[2];
        int n = nums.length;
        // Iterating on all the pairs of the array.
        for(int i = 0; i < n; i++) {
            for(int j = i+1; j < n; j++) {
                int currentPairSum = nums[i] + nums[j];
                if(currentPairSum == target) {   // We got desired pair so we update the indexes in the answer array
                    ans[0] = i;
                    ans[1] = j;
                    break;
                }
            }
            if(ans[1] != 0) break; // If the value of ans[1] is not equal to zero it means that we have found our answer so we can exit the loop.
        }
        return ans;
    }
}
```

> Time Complexity - O(n<sup>2</sup>), as we have used two nested loop

> Space Complexity - O(1)

### Approach 2 - Using HashMap

`Explanation`

nums[i] + nums[j] = target

We can rewrite the above equation as,

nums[j] = target - nums[i]

So now the problem reduces to finding an index j such that the value of array at that index is equal to (target - nums[i]).

We iterate on the array, and for each index i, we check whether an element exists in the array whose value is equal to (target-nums[i]).

Q) Which Data structure tells us whether a value is present in it or not in O(1) time complexity?

Ans) Set and Map data structure tells us whether it contains the given value or not in O(1) time. Now, in this question, we need the index of the value, so we will use the map data structure which will have the key as the array value and the value as the index of that value in the array.

`Algorithm`

1. Create a map.
2. Create an array ans which is used to store the answer.
3. Now iterate on the array nums, and for each index, check whether the value (target-nums[i]) is present in the map or not.
   - If the desired value exists in the map, then we have our answer, so assign the indexes to answer array and break out of the loop.
   - If the value does not exist in the map, we add the current value as key and index as value to the map and continue our search for the answer.

`Code`

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        int ans[] = new int[2];
        int n = nums.length;
        for(int i = 0; i < n; i++) {
            int desiredValue = target-nums[i];
            if(map.containsKey(desiredValue)) {  // Desired value exists in the map
                ans[0] = map.get(desiredValue);
                ans[1] = i;
                break;
            }
            else {
                map.put(nums[i], i);
            }
        }
        return ans;
    }
}
```

> `Time Complexity` - O(n), We have used a loop to iterate on the array, and we are doing constant time work inside the loop.

> `Space Complexity` - O(n), as we have used a map
