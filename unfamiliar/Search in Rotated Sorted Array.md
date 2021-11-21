https://leetcode.com/problems/search-in-rotated-sorted-array/<br>
https://leetcode.com/problems/search-in-rotated-sorted-array-ii/

`These two questions are related so I put them together`

# Question body
```
There is an integer array nums sorted in non-decreasing order.
(with distinct values in the first question)
(not necessarily with distinct values in the second question)

Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].

Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.

You must decrease the overall operation steps as much as possible.
```

# Tips
### Tip 1
#### In the first question, do two binary searches to find the index with the maximum number and the target number

1. Do binary search to find the maximum number (`Find the pattern: nums[X] > nums[X + 1]`)
2. Do binary search to find the target number in the sub-sorted list (`array can be separated to two sorted-lists by index of the maximum number`)

### Tip 2
#### In the first question, observe the pattern of shifted sorted array, do one binary search on the array to find the target number
1. Both right or left shifts have an important pattern:
	1. If the maximum number is at the left side of the middle element:
		* `middle_element < right_element < left_element`
	2. If the maximum number is at the right side of the middle element:
		* `right_element < left_element < middle_element`
2. Because the array before shifting is sorted, the array after shifting has an important pattern:
	1. If the maximum number is at the left side of the middle element:
		* `the sub array at the right side of the middle element is sorted`
	2. If the maximum number is at the right side of the middle element:
		* `the sub array at the left side of the middle element is sorted`
3. If the target number is in the range of the sorted array, recursive in to the sub array. Otherwise, recursive to the other sub array

### Tip 3 `extend Tip 2`
#### In the second question, the number in the array can be indistinct. Need to add one extra judgement in `tip 2`

1. When the middle number can be the same as the left-most number or the right-most number, you can only shift one position to the left or right index in the binary search
	* Example: [1,1,1,3,1] or [1,3,1,1,1], and the target number is 3. You can not decide to go to the left or right side of the array. You can only remove the right-most or left-most element after you check they are not equal to the target number
