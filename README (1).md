# Orthodox canonical class form in C++98 (ex00)

- Default constructor
- Copy constructor
- Destructor
- Copy assignment operator

```
class A final
{
   public:
      A ();
      A (const A &a);
      ~A ();
      A & operator = (const A &a);
};
```
# Floating-point numbers vs Fixed-point numbers
Accuracy = to how close a measurement is to the true value

Precision = how much information you have about a quantity, how uniquely you have it pinned down

Fixed point arithmetic is much faster than floating point arithmetic

## Floating-point

[IEEE-754 Floating Point Converter](https://www.h-schmidt.net/FloatConverter/IEEE754.html)

- s sign bit
- e exponent giving its order of magnitude (= порядок = показатель степени)
- m mantissa specifying the actual digits of the number ∊ [1;10)

Decimal	                        | e                            | m   | float                                            
---------------------------------|------------------------------|-----|--------------------------------------------------
${(-1)}^{s}$ * 1.(mantissa bits) * $2^e$ |                      |     | s eeeeeeee mmmmmmmmmmmmmmmmmmmmmmm 
(1+m/ $2^{23}$ )* $2^{e−127}$    | ~11111111~ ~00000000~        |     |
(0+m/ $2^{23}$ )* $2^{1−127}$    | 00000000                     |     |
Largest $2^{254−127}$ *(1+ ($2^{23}$−1)/ $2^{23}$) = 340282346638528859811704183484516925440 |  |  | 0 11111110 11111111111111111111111   
1234.4321                        |                              |     | 0 10001001 00110100100110111010100
1234.43212890625                 |                              |     | 0 10001001 00110100100110111010100
316014.6250                      |                              |     | 0 10010001 00110100100110111010100
3.14                             | ∊ [ $2^1$ ; $2^2$ ) => $2^7$ | $\frac{3,14 -2 }{4 - 2} *2^{23}$ | 0 10000000 10010001111010111000011
0                                |                              |     | 0 00000000 00000000000000000000000
1.0                              |                              |     | 0 01111111 00000000000000000000000
0.5                              |                              |     | 0 01111110 00000000000000000000000
3                                |                              |     | 0 10000000 10000000000000000000000
1.175494351e-38 smallest without losing precision |             |     | 0 00000001 00000000000000000000000
1.401298464e-45 smallest  	      |                              |     | 0 00000000 00000000000000000000001
1.1929093e-7 the smallest x : 1+x > 1 |                         |     | 0 01101000 00000000001011001110001
+inf                             |                              |     | 0 11111111 00000000000000000000000
-inf                             |                              |     | 1 11111111 00000000000000000000000
+NaN                             |                              | ~0~ | 0 11111111 10000000000000000000000

## Fixed-point

Representing non-integer numbers by storing a fixed number of digits of their fractional part

Example : Dollar amounts are often stored with exactly two fractional digits, representing the cents

$1234.4321_{float}$ = (316014.6176, 8) = (316015, 8) = ($00000000.00000100.11010010.01101111_{2}$, 8) 

# Const object = non-mutable

Attempt to modify it directly -> a compile-time error.

Attempt to modify it indirectly (e.g., by modifying the const object through a reference or pointer to non-const type) -> undefined behavior.

You cannot call a non-const method a const object.

You cannot call a non-const method through a pointer or reference to a const object (regardless of whether the referred-to object is const or not).

Can neither be changed by a const nor a non-const member function (except for constructor and destructor), even if it is passed by reference. There are two exceptions to this rule:
- Ccasting the const away (not advised);
- Class members can be declared using the mutable keyword; these members can be changed through member functions even if the containing object is declared const.

# A static member data member of a class

Is not associated with a particular object.

Belongs to the class rather than objects of the class. 

If it is public, it can be accessed directly using the class name.

Can also be called through objects of the class type, though this is not rechttps://companies.intra.42.fr/en/offersommended.

## A static data member

## A static member function

Has no *this pointer.

Can directly access other static members (variables or functions), but not non-static members, because non-static members must belong to a class object.

In the context of function declarations, static = "this function is scoped only to this file and can't be called from other places".

In the context of member functions, static = "this member function does not have a receiver object. It's basically a normal function that's nested inside of the scope of the class".

Example:
```
class MyClass {
 public:
  static void myfunc();
};

void MyClass::myfunc() {} // do not write 'static'

int main() {
  MyClass::myfunc();
}
```
# Sources
https://www.cprogramming.com/tutorial/floating_point/understanding_floating_point.html

https://www.cprogramming.com/tutorial/floating_point/understanding_floating_point_representation.html

https://www.cprogramming.com/tutorial/floating_point/understanding_floating_point_printing.html

https://stackoverflow.com/questions/60224493/whats-the-largest-number-float-type-can-hold

https://inst.eecs.berkeley.edu//~cs61c/sp06/handout/fixedpt.html 

https://github.com/achrafelkhnissi/CPP_Modules/tree/master

https://github.com/Saxsori/CPP_Modules/tree/main

https://github.com/42YerevanProjects/cpp_modules/tree/master