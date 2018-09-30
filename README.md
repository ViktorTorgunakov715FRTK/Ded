#include <stdio.h>
#include <math.h>
#include <assert.h>
#include <math.h>

/*! This function solves square equation.
 * \param [in] a - coefficient before x * x.
 * \param [in] b - coefficient before x.
 * \param [in] c - constant of square equation.
 * \param [in] root1 - pointer that point on block of memory where first root has to locate.
 * \param [in] root2 - pointer that point on block of memory where second root has to locate.
 */
int Solve_square(double a, double b, double c, double *root1, double *root2);

int Solve_linear(double b, double c, double *root1);
int main( )
{
    using namespace std;
	printf("Square Eq Slv v.1.0 Viktor\n");
	printf("Enter a, b, c:\n");
    double a = NAN, b = NAN, c = NAN;
    int code_scanf = 0xBEDA;
    code_scanf = scanf("%lg %lg %lg", &a, &b, &c);
    while (code_scanf != 3)
    {
        char rubbish;
        while ((rubbish = getchar( )) != '\n');
        printf("You enter incorrect coefficients. Try to enter they again.\n");
        code_scanf = scanf("%lg %lg %lg", &a, &b, &c);
    } 


    double root1 = NAN, root2 = NAN;
    int num_roots = Solve_square(a, b, c, &root1, &root2);
    switch(num_roots)
    {
        case 0:
            printf("Square equation hasn't roots.\n");
            break;
        case 1: 
            printf("Square equation has 1 root: %lg.\n", root1);
            break;
        case 2:
            printf("Square equation has 2 roots: root1 = %lg; root2 = %lg\n.", root1, root2);
            break;
        case 3:
            printf("Each number from the set of real numbers is the solution.\n");
            break;
        default:
            printf("Strange num_root = %d in Solve_square(%lg, %lg, %lg, %p, %p)\n", num_roots, a, b, c, &root1, &root2);
            return 1;
    }
    return 0;
}


int Solve_square(double a, double b, double c, double *root1, double *root2)
{
    assert(isfinite(a));
    assert(isfinite(b));
    assert(isfinite(b));
    assert(root1 != nullptr);
    assert(root2 != nullptr);

    if (a == 0)
    {
        return (Solve_linear(a, b, root1));
    }

    double D = NAN;
    D = b * b - 4 * a * c;
    if (D < 0)
    {
        return 0;
    }
    else if (D == 0)
    {
        *root1 = -b / (2 * a);
        return 1;   
    }
    else if (D > 0)
    {
        *root1 = (-b + sqrt(D)) / (2 * a);
        *root2 = (-b - sqrt(D)) / (2 * a);
        return 2;
    }
    else 
    {
        printf("Strange D = %lg in Solve_square( ), where a = %lg, b = %lg, c = %lg\n", D, a, b, c);
        return 999;
    }
}


int Solve_linear(double b, double c, double *root1)
{
    assert(isfinite(b));
    assert(isfinite(c));
    assert(root1 != nullptr);
    if (b == 0)
    {
        return ((c == 0) * 3);
    }
    else if (b != 0)
    {
        *root1 = -c / b;
        return 1;
    }
    else 
    {
        printf("Strange b = %lg in Solve_linear\n", b);;
        return 999;
    }
}
