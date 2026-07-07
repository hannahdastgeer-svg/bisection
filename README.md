#include <iostream>
#include <stdio.h>
#include <cmath>

#define SQUARE(x) ((x) * (x))  // Function-like macro
#define CUBE(x) ((x) * (x) * (x))  
#define EPSILON 0.01 

double func(double x) { //arbitrary function
    return (CUBE(x) + 2*SQUARE(x) - 2);
}

double bisect(double (*f)(double), double a, double b) {
    double m = (a+b)/2;
    if (fabsf((*f)(m)) <= EPSILON || (b-a) <= EPSILON)
    {
        return m; //base case 
    }
    if (((*f)(a)*(*f)(m)) < 0) //the root lies between a,c
    {
        return bisect(f, a, m);
    }
    if (((*f)(b)*(*f)(m)) < 0) //the root lies between b,c
    {
        return bisect(f, m, b);
    }
    else{
        return -999;
    }
}

int main() {
    double low = 0.0; double high = 5.0;
    double zero = bisect(func, low, high);
    printf("The solution is %.12f\n", zero);
   
    return 0;
}


