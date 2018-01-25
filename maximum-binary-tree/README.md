# Leetcode: Maximum Binary Tree     :BLOG:Basic:


---

Maximum Binary Tree  

---

Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:  

1.  The root is the maximum number in the array.
2.  The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
3.  The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.

Construct the maximum tree by the given array and output the root node of this tree.  

    Example 1:
    Input: [3,2,1,6,0,5]
    Output: return the tree root node representing the following tree:
    
          6
        /   \
       3     5
        \    / 
         2  0   
           \
            1

Note:  
The size of the given array will be in the range [1,1000].  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/maximum-binary-tree)  

Credits To: [leetcode.com](https://leetcode.com/problems/maximum-binary-tree/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: http://brain.dennyzhang.com/maximum-binary-tree
    ## Basic Ideas: recursive way
    ##
    ## Complexity: Time O(n), Space O(1)
    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution(object):
        def constructMaximumBinaryTree(self, nums):
            """
            :type nums: List[int]
            :rtype: TreeNode
            """
            if len(nums) == 0:
                return None
    
            max_index = 0
            for i in xrange(1, len(nums)):
                if nums[i] > nums[max_index]:
                    max_index = i
            root = TreeNode(nums[max_index])
    
            if max_index != 0:
                root.left = self.constructMaximumBinaryTree(nums[0:max_index])
            root.right = self.constructMaximumBinaryTree(nums[max_index+1:])
            return root