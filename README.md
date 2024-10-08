Specific Pair in Matrix in Python
Here, on this page, we will discuss the program to Find a Specific Pair in Matrix in Python Programming language. Given an n x n matrix mat[n][n] of integers, find the maximum value of mat(c, d) – mat(a, b) overall choices of indexes such that both c > a and d > b.

Specific Pair in Matrix in Python

Method Discussed :
Method 1 : Naïve Approach
Method 2 : Efficient Approach
Algorithm ( Method 1 )
For all values mat(a, b) in the matrix
Find mat(c, d) with maximum value such that c > a and d > b and keep updating the maximum value found so far.
Finally return the maximum value.
Time and Space Complexity :
Time complexity: O(N*N)
Space complexity: O(1)
Python Code
Run

N = 5


def findMaxValue(mat):
    maxValue = 0

    for a in range(N - 1):
        for b in range(N - 1):
            for d in range(a + 1, N):
                for e in range(b + 1, N):
                    if maxValue < (mat[d][e] - mat[a][b]):
                        maxValue = mat[d][e] - mat[a][b]
    return maxValue


matrix = [[ 1,  2, -1, -4, -20],
          [-8, -3,  4,  2,   1],
          [ 3,  8,  6,  1,   3],
          [-4, -1,  1,  7,  -6],
          [ 0, -4, 10, -5,   1]]

print("Maximum Value is", findMaxValue(matrix))
Output
Maximum Value is 18
Algorithm ( Method 2 )
In this method, we pre-process the matrix such that index(i, j) stores the max of elements in the matrix from (i, j) to (N-1, N-1) and in the process keeps on updating the maximum value found so far. Then finally return the maximum value.

Python Code
Run

N = 5


def findMaxValue(mat):
    maxValue = -100

    maxArr = [[0] * N for z in range(N)]

    maxArr[N - 1][N - 1] = mat[N - 1][N - 1]
    maxv = mat[N - 1][N - 1]

    for j in range(N - 2, -1, -1):
        if mat[N - 1][j] > maxv:
            maxv = mat[N - 1][j]
        maxArr[N - 1][j] = maxv

    maxv = mat[N - 1][N - 1]

    for i in range(N - 2, -1, -1):
        if mat[i][N - 1] > maxv:
            maxv = mat[i][N - 1]
        maxArr[i][N - 1] = maxv

    for i in range(N - 2, -1, -1):
        for j in range(N - 2, -1, -1):
            if maxArr[i + 1][j + 1] - mat[i][j] > maxValue:
                maxValue = maxArr[i + 1][j + 1] - mat[i][j]
            maxArr[i][j] = max(mat[i][j], max(maxArr[i][j + 1], maxArr[i + 1][j]))

    return maxValue


matrix = [[ 1,  2, -1, -4, -20],
          [-8, -3,  4,  2,   1],
          [ 3,  8,  6,  1,   3],
          [-4, -1,  1,  7,  -6],
          [ 0, -4, 10, -5,   1]]

print("Maximum Value is", findMaxValue(matrix))
Output
Maximum Value is 18
