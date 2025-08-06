# 1679. Max Number of K-Sum Pairs

You are given an integer array nums and an integer k.

In one operation, you can pick two numbers from the array whose sum equals k and remove them from the array.

Return the maximum number of operations you can perform on the array.

---
## Examples

## Example 1:
--- 

Input: nums = [1,2,3,4], k = 5
Output: 2
Explanation: Starting with nums = [1,2,3,4]:
- Remove numbers 1 and 4, then nums = [2,3]
- Remove numbers 2 and 3, then nums = []
There are no more pairs that sum up to 5, hence a total of 2 operations.
## Example 2:
---

Input: nums = [3,1,3,4,3], k = 6
Output: 1
Explanation: Starting with nums = [3,1,3,4,3]:
- Remove the first two 3's, then nums = [1,4,3]
There are no more pairs that sum up to 6, hence a total of 1 operation.



## Brute Force Explanation for "Max Number of K-Sum Pairs"


### Brute Force Code (Commented):
```java
class Solution {
    public int maxOperations(int[] nums, int k) {
    int n = nums.length;
    int countopr = 0;

    // Iterate through each element of the array
    for(int i = 0; i < n; i++) {
        if(nums[i] == -1) continue; // Skip if already removed

        for(int j = i + 1; j < n; j++) {
            if(nums[j] == -1) continue; // Skip if already removed

        // Check if the pair adds up to k
            if(nums[i] + nums[j] == k) {
                nums[i] = -1;  // Mark first element as used
                nums[j] = -1;  // Mark second element as used
                countopr = countopr + 1;  // Increment operation count
            }
        }   
    }


    return countopr; // Final answer: max number of operations
    }
}

# Two Pointer Approach – Explanation

## Approach: Two Pointer (Optimized Solution)

### Prerequisite
- The array must be **sorted** first to use the two-pointer technique.

### Steps
1. **Sort the array `nums`**.
2. Initialize two pointers:
   - `left` pointing to the start of the array
   - `right` pointing to the end of the array
3. Loop while `left < right`:
   - Calculate the `sum = nums[left] + nums[right]`
   - If `sum == k`:  
     - Increment the operation count (`countopr++`)
     - Move both pointers inward (`left++` and `right--`)
   - Else if `sum < k`:  
     - Move `left` pointer to the right (`left++`) to increase the sum
   - Else if `sum > k`:  
     - Move `right` pointer to the left (`right--`) to decrease the sum
4. Return the final count of operations

### Code

```java
import java.util.Arrays;

class Solution {
    public int maxOperations(int[] nums, int k) {
        Arrays.sort(nums);  // Step 1: Sort the array
        int countopr = 0;
        int left = 0;
        int right = nums.length - 1;

        while (left < right) {
            int sum = nums[left] + nums[right];

            if (sum == k) {
                countopr++;
                left++;
                right--;
            } else if (sum < k) {
                left++;
            } else {
                right--;
            }
        }

        return countopr;
    }
}

