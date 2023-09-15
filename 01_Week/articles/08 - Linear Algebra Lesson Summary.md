# Linear Algebra Lesson Summary

Linear algebra is a fundamental branch of mathematics that plays a crucial role in machine learning and data science. In this lesson, we covered essential concepts and operations related to linear algebra, focusing on vector operations, matrix-vector multiplication, matrix-matrix multiplication, identity matrix, and inverse matrix. Here's a detailed summary of the key points:

## Vector Operations

1. **Vector Multiplication**: To multiply a vector by a scalar (e.g., 2), you multiply each element of the vector by that scalar. For example, if you multiply vector `u` by 2, you get `2u = [4, 8, 10, 12]`. Vectors in linear algebra are typically represented as column vectors.

   ```python
   u = np.array([2, 4, 5, 6])
   2 * u
   ```

2. **Vector Addition**: To add two vectors, you simply add their corresponding elements element-wise. For instance, if you add vectors `u` and `v`, you get `u + v = [3, 4, 5]`.

   ```python
   u = np.array([2, 4, 5, 6])
   v = np.array([1, 0, 0, 2])
   u + v
   ```

3. **Dot Product (Inner Product)**: The dot product (also known as the inner product) between two vectors `u` and `v` is a scalar value obtained by multiplying each element of one vector with the corresponding element of the other vector and summing up the results.

   ```python
   u.dot(v)
   ```

## Matrix-Vector Multiplication

1. **Matrix-Vector Multiplication**: When multiplying a matrix `U` by a vector `v`, you compute a new vector where each element is the dot product of a row of the matrix `U` and the vector `v`.

   ```python
   U = np.array([
       [2, 4, 5, 6],
       [1, 2, 1, 2],
       [3, 1, 2, 1],
   ])
   v = np.array([1, 0, 0, 2])
   U.dot(v)
   ```

2. **Dimensionality Matching**: For matrix-vector multiplication to be valid, the number of columns in the matrix (`U`) must match the dimensionality (number of elements) of the vector `v`. If `U` has dimensions `m x n`, `v` must have `n` elements.

## Matrix-Matrix Multiplication

Matrix-matrix multiplication extends the concept of matrix-vector multiplication to multiply two matrices. To multiply matrix `A` by matrix `B`, the number of columns in matrix `A` must match the number of rows in matrix `B`. The resulting matrix `C` will have dimensions `m x p`, where `m` is the number of rows in `A`, and `p` is the number of columns in `B`. The elements of `C` are computed as dot products of rows from `A` and columns from `B`.

   ```python
   U = np.array([
       [2, 4, 5, 6],
       [1, 2, 1, 2],
       [3, 1, 2, 1],
   ])
   
   V = np.array([
       [1, 1, 2],
       [0, 0.5, 1],
       [0, 2, 1],
       [2, 1, 0],
   ])
   
   U.dot(V)
   ```

## Identity Matrix

1. **Identity Matrix**: The identity matrix, denoted as `I`, is a special square matrix where all diagonal elements are 1, and all other elements are 0. Multiplying any matrix by the identity matrix results in the original matrix.

   ```python
   I = np.eye(3)
   ```

   The identity matrix for a given size can be created using `np.eye(n)` for an `n x n` matrix.

## Inverse Matrix

1. **Inverse Matrix**: The inverse of a square matrix `A`, denoted as `A⁻¹`, is another matrix such that when `A` is multiplied by its inverse, the result is the identity matrix `I`.

   ```python
   Vs = V[[0, 1, 2]]  # Extracting a subset of matrix V
   Vs_inv = np.linalg.inv(Vs)  # Calculating the inverse of Vs
   ```

   It's important to note that not all matrices have an inverse. For a matrix to be invertible, its determinant must be nonzero.

This lesson serves as a foundation for understanding more advanced concepts in machine learning and data science, where linear algebra is applied extensively for tasks such as matrix factorization, eigendecomposition, and solving linear systems of equations. Linear algebra is a powerful tool that enables us to manipulate and analyze data efficiently, making it an essential skill for anyone working in the field of data science and machine learning.