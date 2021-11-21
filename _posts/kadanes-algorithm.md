---
title: 'Finding maximum rectangular submatrix'
date: 2021-11-21
permalink: /posts/2021/11/kadanes-algorithm/
tags:
  - kadane's algorithm
  - dynamic programming
---

Given a 2D matrix, find the maximum sum of a rectangular submatrix in it. 

For example, the maximum sum of the matrix is shown below.


And the total value of this maximum submatrix is 15.

As far as we know, Kadane's algorithm is used for finding the maximum subarray in a 1D array in O(n) time complexity: From the beginning, start to accumulate every element it goes through. If at a time, the sum is negative, we will reset the sum to 0, because it is always more beneficial to start from 0 rather than a negative value. I made the gif below to make it easier to understand this approach.


The idea for solving the 2D array is similar: We will fix the two columns of the matrix - the left and the right - one by one. Then, we would consider every row of the matrix (lying between two columns) to be an element in a 1D array and apply Kadane's algorithm to this array.

In other words, we will fix two columns i and j. Let's call b[k] = sum(a[k][i], a[k][i + 1], ..., a[k][j]), we can calculate b[k] efficiently by using prefix sum (for every 0 < k < n). Finally, we use Kadane's algorithm in this array b[]. The time complexity for fixing two columns is O(m^2) because we will loop i and j to m. And while fixing two columns, the time complexity for applying Kadane's algorithm is O(n). Thus, the total time complexity is O(n*m^2). If it is a square matrix (n = m), then the total time complexity is O(n^3).

Check the code below!
* Kadane's algorithm: https://ideone.com/LmvCUl
* 2D maximum submatrix: https://ideone.com/DgsqtC
