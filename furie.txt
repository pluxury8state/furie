#define _CRT_SECURE_NO_WARNINGS
#include <math.h>
#include <iostream>
#include "Furie.h"
using namespace std;


void dft(double *inarray, double **outarray, int N){

    double pi = 3.14159;

    for (int k = 0; k < N; k++) {
        outarray[0][k] = 0.0;
        outarray[1][k] = 0.0;
        for (int n = 0; n < N; n++) {
            outarray[0][k] += inarray[n] * cos((2 * pi * n * k) / N);
            outarray[1][k] -= inarray[n] * sin((2 * pi * n * k) / N);
        }
    }

}


int main()
{
    int N;
    cout << "Enter the value of N :";
    cin >> N;
    cout << "\n";

    double* inarray = NULL;  //input array
    inarray = new double[N];
    
    // inicialisation
    for (int i = 0; i < N; i++) {
        inarray[i] = rand();
        cout << inarray[i] << "\t";
    }
    cout << "\n\n";
    


    int two_dem_size = 2;
    double** outarray = new double* [two_dem_size]; // rows for real and imagine values
    for (int i = 0; i < two_dem_size; i++) {
        outarray[i] = new double[N];
    }
   
    cout << "function work: \n";

    dft(inarray, outarray, N);

    //output
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < N; j++) {
            cout << outarray[i][j] << "  ";
        }
        cout << "\n";
    }


    delete[] inarray;
    for (int i = 0; i < 2; i++) {
        delete [] outarray[i];
    }
    delete[] outarray;

    return 0;
}