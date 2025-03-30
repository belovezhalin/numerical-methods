# Task E
## SOR - Successive Over-Relaxation Method
### Programming Language: C++

The Successive Over-Relaxation (SOR) method is an iterative technique for solving systems of linear equations:

\[ Ax = y \]

where \( A \in \mathbb{R}^{N \times N} \), \( x, y \in \mathbb{R}^N \).

For a given parameter \( \omega \) and an initial vector \( x_0 \), the method generates a sequence of approximations \( x_k \).

For symmetric, positive definite matrices and \( \omega \in (0, 2) \), the SOR method converges to the solution of the given system for any starting vector.

The goal of this task is to implement the SOR method for systems where matrix \( A \) is a symmetric sparse matrix (most elements are zero) with a banded structure. This means that nonzero elements appear on the diagonal and within a certain number of "bands" above and below the diagonal. If the number of bands above the diagonal is \( M \), then in row \( k \), nonzero elements can be found at positions \( a_{k,j} \) where \( k - M \leq j \leq k + M \).

### Example Matrix

A sample matrix \( B \) (size \( N=8 \) with \( M = 2 \)) may look as follows:

\[
B = \begin{bmatrix}
    c_1 & b_1 & a_1 & 0 & 0 & 0 & 0 & 0 \\
    b_1 & c_2 & b_2 & a_2 & 0 & 0 & 0 & 0 \\
    a_1 & b_2 & c_3 & b_3 & a_3 & 0 & 0 & 0 \\
    0 & a_2 & b_3 & c_4 & b_4 & a_4 & 0 & 0 \\
    0 & 0 & a_3 & b_4 & c_5 & b_5 & a_5 & 0 \\
    0 & 0 & 0 & a_4 & b_5 & c_6 & b_6 & a_6 \\
    0 & 0 & 0 & 0 & a_5 & b_6 & c_7 & b_7 \\
    0 & 0 & 0 & 0 & 0 & a_6 & b_7 & c_8 \\
\end{bmatrix}
\]

## Input Format

The input data is structured as follows:

```
N
M
first band
second band
...
M-th band
diagonal
equation right-hand side
initial vector
ω
L
```

where:
- \( N \) is the matrix size,
- \( M \) is the number of nonzero bands,
- \( \omega \) is the SOR method parameter,
- \( L \) is the number of iterations to perform.

### Example Input (for matrix B):
```
8
2
a1 a2 a3 a4 a5 a6
b1 b2 b3 b4 b5 b6 b7
c1 c2 c3 c4 c5 c6 c7 c8
y1 y2 y3 y4 y5 y6 y7 y8
x0_1 x0_2 x0_3 x0_4 x0_5 x0_6 x0_7 x0_8
1.5
4
```
This defines a task to perform 4 iterations of the SOR method for the system \( Bx = y \), where \( y = (y_1, y_2, ..., y_8) \), \( \omega = 1.5 \), and initial vector \( x_0 = (x_0_1, x_0_2, ..., x_0_8) \).

## Output Format

The output should contain the coordinates of the vector \( x_L \) obtained after performing \( L \) iterations of the SOR method for the given input data. Results should be printed in scientific notation with a precision of 10 decimal places.

### Example Output
```
x4_1
x4_2
x4_3
x4_4
x4_5
x4_6
x4_7
x4_8
```

## Notes

Due to rounding errors, results will be compared with an allowable error margin, both relative (\( \varepsilon_r \), typically around \( 10^{-8} \)) and absolute (\( \varepsilon_a \), typically around \( 10^{-12} \)). Specifically, if the expected result is \( x \) and the program returns \( \tilde{x} \), the result will be rejected if:

\[ |x - \tilde{x}| > \varepsilon_a \] and \[ \left| \frac{x - \tilde{x}}{x} \right| > \varepsilon_r \]

## Example Cases

### Input (file1.in)
```
7
2
1 2 1 2 1
2 -1 3 1 3 -1
5 6 7 8 9 10 11
8 9 11 16 15 14 11
2 3 2 3 2 3 2
1.5
1
```

### Expected Output (file1.out)
```
-1.0000000000000000e+000
2.5000000000000000e-001
-7.3214285714285721e-001
3.1808035714285765e-001
-2.6432291666666696e-001
9.2352120535714288e-001
6.6197874391233791e-001
```

### Input (file2.in)
```
10
1
1 -1 2 1 3 -1 1 2 2
8 9 10 9 8 5 10 9 7 5
7 -8 5 -7 3 -5 7 -5 4 -3
2 1 2 1 2 1 2 1 2 1
1.3
5
```

### Expected Output (file2.out)
```
9.9940568551471820e-01
-9.0904662229329669e-01
6.0991796223201045e-01
-1.0130102944878934e+00
1.0831324689900357e+00
-1.5137961825745920e+00
6.1540772283026224e-01
-8.7787343355916414e-01
1.1233322463475970e+00
-1.0523066239504728e+00
```
