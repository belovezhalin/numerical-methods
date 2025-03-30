# GeomSeq

The task is to find three numbers `x_1, x_2, and x_3` that form a geometric sequence where `x_1 >= x_3` given the sum `S = x_1 + x_2 + x_3` and the product `P = x_1 * x_2 * x_3`. 

If it is not possible to find these numbers (e.g., due to incorrect input data), the expected output is `0.0 0.0 0.0`.

## Notes:
- Only `float` data types are allowed. Using `double` will result in a rejection of the solution.
- Results must be printed in scientific notation with 10 significant digits.
- Results are considered correct if the absolute error for each number is less than 10^{-25} or the relative error does not exceed 10^{-6}.

## Input Format:
```
N
P1 S1
...
PN SN
```
Where:
- N is the number of sequences.
- P_i and S_i are the product and sum of the first three terms of the i-th geometric sequence.

## Output Format:
```
a1 b1 c1
...
aN bN cN
```
Where:
- a_i, b_i, and c_i are the terms of the i-th geometric sequence such that `a_i >= c_i`. If no sequence exists, return `0.0 0.0 0.0`.

## Example:

### Input:
```
9
1.0000000000e+00 3.0000000000e+00
6.4000000000e+01 2.1000000000e+01
-6.4000000000e+01 -2.1000000000e+01
6.4000000000e+01 -1.3000000000e+01
-6.4000000000e+01 1.3000000000e+01
1.0000000150e+30 1.0000000200e+20
1.0000000150e+30 -1.0000000200e+20
0.0000000000e+00 0.0000000000e+00
1.0000000000e+02 1.0000000000e+00
```
### Output:
```
1.0000000000e+00 1.0000000000e+00 1.0000000000e+00
1.6000000000e+01 4.0000000000e+00 1.0000000000e+00
-1.0000000000e+00 -4.0000000000e+00 -1.6000000000e+01
-1.0000000000e+00 4.0000000000e+00 -1.6000000000e+01
1.6000000000e+01 -4.0000000000e+00 1.0000000000e+00
1.0000000200e+20 1.0000000000e+10 1.0000000000e+00
-1.0000000000e+00 1.0000000000e+10 -1.0000000200e+20
0.0000000000e+00 0.0000000000e+00 0.0000000000e+00
0.0000000000e+00 0.0000000000e+00 0.0000000000e+00
```
