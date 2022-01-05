---
title: "Kadane's algorithm - Finding maximum rectangular submatrix"
date: 2021-07-13
permalink: /posts/kadanes-algorithm/
tags:
  - kadanes algorithm
  - dynamic programming
---

Given a 2D matrix, find the maximum sum of a rectangular submatrix in it. 

For example, the maximum sum of the matrix is shown below.

<div align="center">
  <img src="https://lh3.googleusercontent.com/-7gH58TTJtPc/X_eapQkl1pI/AAAAAAAACU0/4Xf01_Ojeo0PTn-w9ahwvdv219-UIYsRQCLcBGAsYHQ/image.png" alt="2D Matrix">
</div>


And the total value of this maximum submatrix is 15.

As far as we know, Kadane's algorithm is used for finding the maximum subarray in a 1D array in O(n) time complexity: From the beginning, start to accumulate every element it goes through. If at a time, the sum is negative, we will reset the sum to 0, because it is always more beneficial to start from 0 rather than a negative value. I made the gif below to make it easier to understand this approach.

```
// kadane's algorithm
int sum = 0, ans = 0;
for (int i = 0; i < n; i++) {
    sum += a[i];
    ans = max(ans, sum);
    if (sum < 0) sum = 0;
}
```

<div align="center">
  <img src="https://i.imgur.com/E3oJPyY.gif" alt="Kadane's algorithm">
</div>

The idea for solving the 2D array is similar: We will fix the two columns of the matrix - the left and the right - one by one. Then, we would consider every row of the matrix (lying between two columns) to be an element in a 1D array and apply Kadane's algorithm to this array.

In other words, we will fix two columns i and j. Let's call b[k] = sum(a[k][i], a[k][i + 1], ..., a[k][j]), we can calculate b[k] efficiently by using prefix sum (for every 0 < k < n). Finally, we use Kadane's algorithm in this array b[]. The time complexity for fixing two columns is O(m^2) because we will loop i and j to m. And while fixing two columns, the time complexity for applying Kadane's algorithm is O(n). Thus, the total time complexity is O(n*m^2). If it is a square matrix (n = m), then the total time complexity is O(n^3).

```
// calculate prefix sum
for (int i = 0; i < n; i++) {
    for (int j = 0; j < m; j++) {
        cin >> a[i][j];
        if (j > 0) a[i][j] += a[i][j - 1]; // prefix sum for i-th row
    }
}

// kadane's for 2D array
int ans = 0;
for (int i = 0; i < m; i++) { // fix i
    for (int j = i + 1; j < m; j++) { // fix j
        int sum = 0;
        for (int k = 0; k < n; k++) { // iterate from first row to last row
            sum += a[k][j];
            if (i > 0) sum -= a[k][i - 1];
            ans = max(ans, sum);
            if (sum < 0) sum = 0;
        }
    }
}
```

Check the full code below!
* Kadane's algorithm: <a href="https://ideone.com/LmvCUl" target="_blank">https://ideone.com/LmvCUl</a>
* 2D maximum submatrix: <a href="https://ideone.com/DgsqtC" target="_blank">https://ideone.com/DgsqtC</a>
