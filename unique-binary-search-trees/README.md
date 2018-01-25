# Leetcode: Unique Binary Search Trees     :BLOG:Hard:


---

Unique Binary Search Trees  

---

Given n, how many structurally unique BST's (binary search trees) that store values 1&#x2026;n?  

    For example,
    Given n = 3, there are a total of 5 unique BST's.
    
       1         3     3      2      1
        \       /     /      / \      \
         3     2     1      1   3      2
        /     /       \                 \
       2     1         2                 3

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/unique-binary-search-trees)  

Credits To: [leetcode.com](https://leetcode.com/problems/unique-binary-search-trees/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: http://brain.dennyzhang.com/unique-binary-search-trees
    #!/usr/bin/env python
    ## Basic Ideas: dynamic programming
    ##       Pitfalls: try to compare the values. This direction will make things very complicated
    ##
    ##       How to get f(n) from previous values?
    ##           1. We will have a root, so sum(left sub-tree nodes) + sum(right sub-tree nodes) = n-1
    ##           2. If root is i, left sub-tree will have i-1 nodes, right sub-tree will have n-k nodes.
    ##                  How many different types? f(i-1)*f(n-i)
    ##           3. Loop k from 1 to n. Then collect the total number
    ##  n = 2:
    ##
    ##       1         2
    ##        \       /
    ##         2     1
    ##
    ##  n = 3:
    ##
    ##       1         3     3      2      1
    ##        \       /     /      / \      \
    ##         3     2     1      1   3      2
    ##        /     /       \                 \
    ##       2     1         2                 3
    ##
    ##  n = 4:
    ##
    ##
    ##
    ## Complexity:
    class Solution(object):
        def numTrees(self, n):
            """
            :type n: int
            :rtype: int
            """
            if n == 0: return 1
            if n == 1: return 1
            l = [None] * (n+1)
            l[1], l[0] = 1, 1
    
            # calculate value
            for k in range(2, n+1):
                count = 0
                # how many nodes we can choose for left sub-tree
                for i in range(0, k):
                    count += l[i]*l[k-1-i]
                l[k] = count
            return l[n]
    
    s = Solution()
    print s.numTrees(4) # 14