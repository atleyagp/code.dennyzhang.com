# Leetcode: Diagonal Traverse     :BLOG:Basic:


---

Diagonal Traverse  

---

Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.  

    Example:
    Input:
    [
     [ 1, 2, 3 ],
     [ 4, 5, 6 ],
     [ 7, 8, 9 ]
    ]
    Output:  [1,2,4,7,5,3,6,8,9]

Note:  
The total number of elements of the given matrix will not exceed 10,000.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/diagonal-traverse)  

Credits To: [leetcode.com](https://leetcode.com/problems/diagonal-traverse/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: http://brain.dennyzhang.com/diagonal-traverse
    #!/usr/bin/env python
    ## Basic Ideas:
    ##      Don't get confused with 2 things:
    ##        1. For coordinate in math, move one step down from (0, 0), we will get (0, -1)
    ##           Move one step down from matrix[i][j], we shall get matrix[i+1][j].
    ##           It's neither matrix[i][j+1] nor matrix[i][j-1]
    ##
    ##        2. In matrix[i][j], i indicates row_index, and j indicates col_index.
    ##           In (x, y), x indicates col_index, y indicates row_index
    ##
    ##        Starts with (0, 0)
    ##                 Sequence                 Move to next               When to stop              How to update starting position
    ##              +: (0, 0)                   m[i][j] -> m[i-1][j+1]    first row or last column   next node in clockwise position
    ##              -: (1, 0) (0, 1)            m[i][j] -> m[i+1][j-1]    first column or last row    next node in counter clockwise position
    ##              +: (0, 2) (1, 1) (2, 0)     m[i][j] -> m[i-1][j+1]
    ##              -: (2, 1) (1, 2)            m[i][j] -> m[i+1][j-1]
    ##              +: (2, 2)                   
    ##
    ## Complexity: Time O(n*n), Space O(1)
    class Solution(object):
        def findDiagonalOrder(self, matrix):
            """
            :type matrix: List[List[int]]
            :rtype: List[int]
            """
            row_count = len(matrix)
            if row_count == 0:
                return []
            col_count = len(matrix[0])
            res = [None] * (row_count * col_count)
    
            i, j, is_up = 0, 0, True
            for k in xrange(row_count * col_count):
                res[k] = matrix[i][j]
                if is_up:
                    if i == 0 or j == col_count-1:
                        is_up = not is_up
                        if j != col_count - 1:
                            j = j+1
                        else:
                            i = i+1
                    else:
                        i, j = i-1, j+1
                else:
                    if j == 0 or i == row_count-1:
                        is_up = not is_up
                        if i != row_count -1:
                            i = i+1
                        else:
                            j = j+1
                    else:
                        i,j = i+1, j-1
            return res
    
    s = Solution()
    print s.findDiagonalOrder([[1, 2, 3], [4, 5, 6], [7, 8, 9]]) #[1,2,4,7,5,3,6,8,9]