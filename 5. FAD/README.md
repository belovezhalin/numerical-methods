## FAD2 - Mixed Derivatives

**Programming Language:** C++

Symbolic computation of successive derivatives of a given function \( f: \mathbb{R}^2 \to \mathbb{R} \) quickly leads to very complex formulas, which in turn cause large numerical errors. Often, we do not have an explicit formula for the function, but rather its values are computed by a subprogram. Therefore, in automatic differentiation, basic arithmetic operations and elementary functions are replaced with corresponding operations and functions that operate on sequences of Taylor series coefficients (or values of successive derivatives), called function jets. For this reason, the techniques presented here are referred to as **jet propagation**.

The goal of this task is to implement jets for computing all derivatives of a function of two variables up to the second order at a given point. That is, for a given function \( f(x, y) \) and point \( (x_0, y_0) \), we need to compute:

\[
\left( f(x_0, y_0), f_x(x_0, y_0), f_y(x_0, y_0), f_{xx}(x_0, y_0), f_{xy}(x_0, y_0), f_{yy}(x_0, y_0) \right)
\]

## Input

The task involves computing the function values and all partial derivatives up to the second order for a given function at \( M \) points \( (x_1, y_1), (x_2, y_2), \dots, (x_M, y_M) \) where \( 0 < M < 1,000,000 \).

The program input follows this format:

```
M
x1 y1
x2 y2
...
xM yM
```

The function is defined in the `function.h` file as a template with the following signature:

```cpp
template <typename T>
T function(const T& x, const T& y);
```

The type `T` is expected to support the following operations:
- `+`, `-`, `*`, `/` between objects of type `T`,
- `+`, `-`, `*`, `/` between a constant and an object of type `T`,
- Unary negation `-`,
- Elementary functions: `sin`, `cos`, `exp`,
- Assignment operator,
- Default constructor (initializing to `0`) and copy constructor.

## Output

For each input point, the program should print, on a separate line, the function value followed by the derivatives in the order:

```
f(x1, y1) fx(x1, y1) fy(x1, y1) fxx(x1, y1) fxy(x1, y1) fyy(x1, y1)
...
f(xM, yM) fx(xM, yM) fy(xM, yM) fxx(xM, yM) fxy(xM, yM) fyy(xM, yM)
```

## Notes

Due to rounding errors, results will be compared against a permissible relative error \( \varepsilon_r \) and absolute error \( \varepsilon_a \) (typically around \( 10^{-8} \)). Specifically, if the expected result is \( x \) and the program returns \( \bar{x} \), the result will be rejected if:

\[
|x - \bar{x}| > \varepsilon_a \quad \text{and} \quad \left| \frac{x - \bar{x}}{x} \right| > \varepsilon_r \quad \text{for} \quad x \neq 0.
\]

## Example

**File `function.h`**:

```cpp
template <typename T>
T function(const T& x, const T& y) {
    T result = sin(x * x - 2 * (y + 1)) / exp(-y * y + cos(x * y));
    return result;
}
```

**For input (test0/0):**

```
4
0.0 1.0
1.0 -1.0
-2.0 2.0
10.0 0.1
```

**Exact output to 15 decimal places (computed symbolically by Mathematica):**

```
0.756802495307928  0.000000000000000  2.82089223234308  -0.550484746419296  0.000000000000000  6.74275395752475
1.332549397776314  2.83254191138382  -5.49764070691010  0.924483034856005  -5.99962825432166  18.5387068096272
-95.4459944863016  30.2587880515848  -149.953283536275  1999.5898972416  649.252143179076  84.8188819463636
-0.23489123252023  -10.8099926844176  -0.944497087145179  91.0586053228664  -102.754369536573  -11.062545637455
```

(In the above table, lines have been broken; the output should have four lines.)

