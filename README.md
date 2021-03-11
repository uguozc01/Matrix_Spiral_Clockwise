# TASK :
    
    Write a program which prints/returns the elements of a 2D matrix in a clockwise, spiral order.


# ABSTRACT:

    Writing a short code does not always mean it is a good quality code in terms of performance. 
    Equally writing a bit longer code does not mean it is a bad code!

    Numpy array is densely packed in memory due to its homogeneous type, it also frees the memory faster. 
    So overall a task executed in Numpy is around 5 to 100 times faster than the standard python list


# SOLUTION:

    On the internet you will see many solutions for this particular algorithm where people will be mostly 
    using loop inside loops, like the following:

    ```python
        for i in range..
            for j in range..

    # O(n^2) time complexity
    # or same looping different way of showing:

        for i in range(r * c)    # where r, c are row and columns.
    ```

    so for a 200 x 100 matrix let's calculate how many loops you need! 
    
    ** loops = 200 * 100 = 20,000 ** times!

    However, I have found a very efficient way to decrease the time complexity O(N).
    The advantage of my approach is there is no loop inside loops. There is only a certain number
    of loops (k times of 4, k is integer) have to be used depending on the shape of the matrix.
    If you provide an enormous 200 x 100 size matrix or bigger there will be a significant 
    decrease in spent time for calculations compared to those O(n^2) solutions.

    Let's now calculate the required loops according to my approach, we will only need 

        ** road = 2 * len(M) - 1 **          __which yields 199__
        ** loop_count = (road // 4) + 1 **
        ** loop_count = 199 // 4  + 1 **         __which is 50 times, so it means 200 times less looping!__


# Algorithm:

    In order to prove my approach, please go ahead and get a piece of paper and a pen 
    and start drawing to see the algorithm yourself with the following instructions, I did so!
    
    When a matrix shape is **n x (n+k)** where **k >= 0**, then we will always cover **2n -1** times road, 
    in other words ** (2* len(M) - 1) ** times. 
    Observe this by starting from (0,0) and covering elements of matrix clockwise in a spiral order.
    Use 4x4,5x5 or 6x6 shape matrices first and then 4x5, 5x6 or 6x7 size matrices respectively.

    When the row count is more than column count (height is larger than width), which means (n+k) x n size matrix, 
    then we have to always cover 2*n times road (slicing) in other words (2 * len(M[0]) times. 
    Test and see this yourself by using 5x4, 6x5 or 7x6 shape matrices on a paper by drawing spirals.

    I used Numpy to slice all rows and columns. Then after each slicing, I redefined the leftover matrix (by removing the sliced part). 
    I have kept track of positional parameters i,j to see where our pointer is. 
    I have also kept track of row, column counts r,c for last 2x2 comparison.