## Solving Systems of Linear Equations Using Gaussian Elimination

Gaussian elimination is commonly used to solve systems of linear equations. Due to the inaccuracy of numerical representation and rounding errors, the results obtained using the basic version of this method may not be precise. Therefore, several modifications are considered, including selecting pivot elements and iteratively refining the solution.

### Task
The task is to implement a function with the following signature:

```cpp
Vector solveEquations(
        const Matrix & A,   // Matrix
        const Vector & b,   // Vector
        double  eps         // Acceptable error
);
```

The function should use Gaussian elimination to solve the system of linear equations:

\[ A x = b \]

where \( A \) is an \( n \times n \) square matrix, and \( x \) and \( b \) are vectors of size \( n \). The maximum size is \( n = 3000 \). (The size \( n \) can be retrieved using the `size` methods of both the vector and matrix.) We assume that the given system has exactly one solution.

To pass all tests, the implementation must follow these constraints:
- Use Gaussian elimination with **scaled partial pivoting**.
- Compute row scales only once at the beginning of the algorithm.
- Refine the solution iteratively until the required accuracy is achieved.

### Submission Guidelines
Submit a file named `source.cpp` containing the definition of the `solveEquations` function and any helper functions, but **without** a `main` function. The testing programs will compile using the following command:

```sh
g++ test.cpp source.cpp -O2 -std=c++11 -o test
```

A sample test program is provided below, along with example input and expected output.

### Solution Accuracy Evaluation
The `solveEquations` function should return a vector \( x \) that satisfies the equation with accuracy `eps`, measured using the **maximum norm**:

\[ \text{residual\_vector}(A, b, x).\text{max\_norm()} < \text{eps} \]

The returned solution and the residual vector printed by the sample test may differ from the expected output. The critical requirement is that the above condition is met.

### Vector and Matrix Representation
A simple implementation of `Vector` and `Matrix` classes is provided for convenience. Their definitions are included in the `vectalg.h` header file. **Do not submit this file**; it will be available in the testing system.

#### Example Usage
```cpp
#include <iostream>
#include "vectalg.h"
using namespace std;

int main() {
    Matrix A(4);   // Uninitialized 4x4 matrix
    Matrix B {{1., 2.},{1.4, 1.23}}; // 2x3 matrix initialized with data
    A = B;         // A is now equal to B
    Matrix C(A);   // Copy constructor
    A(0,0) = 5;    // Modify an element at (0,0)
    cout << A << endl;
    cout << C << C.size() << endl;
   
    Vector v(3);
    v[0] = -1; v[1] = 9; v[2] = 10;  // Access elements
    Vector w = {1,2,3,5};
    cout << v << endl;
    cout << w << endl;
    cout << v.max_norm() << v.size() << endl;
    // v[3] = 4; // ERROR!
    return 0;
}
```

### Sample Tests

#### Test Program
```cpp
#include "source.cpp"
#include <iostream>
#include "vectalg.h"
using namespace std;

Vector solveEquations(
        const Matrix & A,
        const Vector & b,
        double  eps
);

int main(){
    cout.precision(17);
    int n = 0;
    double eps = 0;

    // Read input
    cin >> n;
    Matrix a(n);
    Vector b(n);
    cin >> a >> b >> eps;

    Vector x = solveEquations(a, b, eps);

    auto residual = residual_vector(a, b, x);
    cout << "solution = " << x << endl;
    cout << "residual = " << residual << endl;
    cout << "error = " << residual.max_norm()
         << " limit = " << eps << endl;
    cout << "Test " << (residual.max_norm() < eps ? "":"not ") << "passed" << endl; 
    return 0;
}
```

#### Input Format
```
n
A
b
eps
```

#### Example 1
**Input:**
```
2
1 1
1 -1
1
1
1e-15
```
