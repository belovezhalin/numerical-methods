# Interpolation Using Spline Functions

Interpolation using spline functions involves drawing a curve of a specified type through a given set of points.

## Task Description

The task is to write a C++ class:

```cpp
class spline {
public:
    spline(int n);
    void set_points(double x[], double y[]);
    double operator()(double z) const;
};
```

which, for given nodes \((x[i], y[i])\), calculates the values of a natural cubic spline function.

### Class Details:

- The constructor takes the number of nodes `n` as an argument.
- The method `set_points(double x[], double y[])` loads the nodes \((x[i], y[i])\) and determines the spline function based on them.
- Assumptions:
  - The array `x` is sorted in ascending order.
  - The second derivatives at the boundary nodes `x[0]` and `x[n-1]` are zero (the natural spline condition).
- The overloaded `operator()` returns the value of the spline function at a given point `z`.
- It is assumed that `z` belongs to the interval \([x[0], x[n-1]]\).

The solution should be submitted as `source.cpp` and `source.h`, containing the implementation of the class and any auxiliary functions but excluding the `main` function.

## Example Usage

```cpp
#include <iostream>
#include <vector>
#include "spline.h"

using namespace std;

int main(int argc, char** argv) {
    cout.precision(15);
    cout << fixed;
  
    int size = 6;
    double X[] = {0, 0.2, 0.4, 0.6, 0.8, 1};
    double Y[] = {-3, -2.56, -2.04, -1.44, -0.76, 0};

    spline s(size);
    s.set_points(X, Y);    
   
    for(int i = 0; i < size - 1; i++) {
        std::cout << s(X[i]) << "  " << s(X[i] + 0.02) << "  " << s(X[i] + 0.07) << std::endl;
    }
    
    return 0;
}
```

### Expected Output:

```
-3.000000000000000  -2.957667368421053  -2.851172631578947
-2.560000000000000  -2.512130526315790  -2.388201578947368
-2.040000000000000  -1.983410526315790  -1.838621052631579
-1.440000000000000  -1.375827368421052  -1.211914210526316
-0.760000000000000  -0.686880000000000  -0.500322105263158
```

### Performance Consideration:

Test 3 verifies the program's performance for **10,000 nodes**.

