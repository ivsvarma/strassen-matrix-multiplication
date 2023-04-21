# strassen-matrix-multiplication
Strassen’s Matrix Multiplication is the divide and conquer approach to solve the matrix multiplication problems. The usual matrix multiplication method multiplies each row with each column to achieve the product matrix. The time complexity taken by this approach is O(n3), since it takes two loops to multiply

#include <iostream>
#include <vector>

using namespace std;

vector<vector<int>> matrixAddition(const vector<vector<int>>& A, const vector<vector<int>>& B) {
    int n = A.size();
    vector<vector<int>> C(n, vector<int>(n, 0));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            C[i][j] = A[i][j] + B[i][j];
        }
    }
    return C;
}

vector<vector<int>> matrixSubtraction(const vector<vector<int>>& A, const vector<vector<int>>& B) {
    int n = A.size();
    vector<vector<int>> C(n, vector<int>(n, 0));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            C[i][j] = A[i][j] - B[i][j];
        }
    }
    return C;
}

vector<vector<int>> strassen(const vector<vector<int>>& A, const vector<vector<int>>& B) {
    int n = A.size();
    vector<vector<int>> C(n, vector<int>(n, 0));
    if (n == 1) {
        C[0][0] = A[0][0] * B[0][0];
        return C;
    } else {
        vector<vector<int>> A11(n/2, vector<int>(n/2));
        vector<vector<int>> A12(n/2, vector<int>(n/2));
        vector<vector<int>> A21(n/2, vector<int>(n/2));
        vector<vector<int>> A22(n/2, vector<int>(n/2));
        vector<vector<int>> B11(n/2, vector<int>(n/2));
        vector<vector<int>> B12(n/2, vector<int>(n/2));
        vector<vector<int>> B21(n/2, vector<int>(n/2));
        vector<vector<int>> B22(n/2, vector<int>(n/2));
        for (int i = 0; i < n/2; i++) {
            for (int j = 0; j < n/2; j++) {
                A11[i][j] = A[i][j];
                A12[i][j] = A[i][j+n/2];
                A21[i][j] = A[i+n/2][j];
                A22[i][j] = A[i+n/2][j+n/2];
                B11[i][j] = B[i][j];
                B12[i][j] = B[i][j+n/2];
                B21[i][j] = B[i+n/2][j];
                B22[i][j] = B[i+n/2][j+n/2];
            }
        }
        vector<vector<int>> S1 = matrixSubtraction(B12, B22);
        vector<vector<int>> S2 = matrixAddition(A11, A12);
        vector<vector<int>> S3 = matrixAddition(A21, A22);
        vector<vector<int>> S4 = matrixSubtraction(B21, B11);
        vector<vector<int>> S5 = matrixAddition(A11, A22);
        vector<vector<int>> S6 = matrixAddition(B11, B22);
        vector<vector<int>> S7 = matrixSubtraction(A12, A22);
        vector<vector<int>> S8 = matrixAddition(B21, B
