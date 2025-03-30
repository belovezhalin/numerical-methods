# Bisection and Secant Methods

In theory, the **Bisection method** always finds the root of a function if we start with two points where the function has opposite signs. However, it converges slowly. On the other hand, the **Secant method** converges faster but only locally.

## Task

Write a C++ function with the following signature:

```cpp
double findZero(
    double (*f)(double),  // function whose zero we are looking for in [a, b]
    double a,              // left end of the interval
    double b,              // right end of the interval
    int M,                 // maximum allowed number of function calls
    double eps,            // expected accuracy of the root
    double delta           // sufficient absolute error of the result
);
```
This function combines both methods (Bisection and Secant) to provide a method that performs well globally and locally.

## Function Details:
The function takes in a continuous function f and an interval [a, b] to find the zero.

If f(a) * f(b) ≤ 0, the root should be within [a, b]. Otherwise, the Secant method starts with x0 = a and x1 = b.

The function must call f at most M times. Exceeding this limit will result in an execution error.

The root is accepted if |f(x0)| ≤ eps or |x - x0| ≤ delta, where x is the exact root of the function.

## Goal:
Implement a function that combines the Bisection and Secant methods to find a zero of a nonlinear function efficiently.
