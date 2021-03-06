#flashcards/circom

# Signals

## Signals

What are circom circuits built over?
?
Signals.
<!--SR:2022-09-09,57,210-->

What do signals contain?
?
Field elements in $\mathbb{Z}/p\mathbb{Z}$
<!--SR:2022-09-29,87,250-->

What are the kinds of signals?
?
Input, output, and intermediate.
<!--SR:2022-09-22,69,210-->

How do you declare an input signal?
?
`signal input in;` declares an input signal named `in`
<!--SR:2022-07-28,44,230-->

How do you declare an output signal?
?
`signal output out;` declares an output signal named `out`
<!--SR:2022-10-31,103,250-->

How do you declare an intermediate signal?
?
`signal inter;` declares an intermediate signal named `inter`.
<!--SR:2022-09-29,86,250-->

How do you declare an array of output signals?
?
`signal output out[N];` declares an array of length `N` called `out` containing output signals.
<!--SR:2022-09-29,79,230-->

When are signals private vs public?
?
All output signals of the main component are public and can't be made private.
Input signals of the main component are private by default but can be declared private.
The rest of the signals are private and can't be made public.
<!--SR:2022-09-20,57,230-->

How would we declare public inputs for a component made by a template called `Multiplier2` with two public inputs `in1` and `in2`?
?
`component main{public [in1, in2]} = Multiplier2();`
<!--SR:2022-08-03,44,230-->

How can we rewrite the lines:
```
signal output out;
out <== in1 * in2;
```
?
`signal output out <== in1 * in2`
<!--SR:2022-08-04,49,250-->

How do we instantiate a component?
?
```
template B() {
	component someName = A();
}
<!--SR:2022-08-25,64,250-->

template A(){
	...
}
```

How do we access the output of a component?
?
```
template B(){
	component comp = A();
	someSignal <== A.outA
}
<!--SR:2022-10-08,88,250-->

template A(){
	...
	signal output outA
}
```

What happens if try to access a non output signal on a component?
?
Compile error.
<!--SR:2022-09-08,73,250-->

What is wrong with the following code?
```
out <== 0;
component comp A();
out <== comp.outA;
```
?
Signals are immutable, so assigning to `out` twice gives a compilation error.
<!--SR:2022-09-18,79,250-->

What operators can be used to assign signals?
?
`<--`, `<==`, `-->`, or `==>`.
<!--SR:2022-07-27,43,230-->

What's the difference between `==>` and `<==` vs `<--` and `-->`?
?
`==>` and `<==` add a constraint, making them the safer option.
<!--SR:2022-09-23,80,250-->

What's an example of when we must use `<--` rather than `<==` and what does it do?
?
`out[k] <-- (in >> k) & 1`
Puts the `k`th digit of `in` in `out[k]`. Right shift moves the `k`th bit to the end of the number, and `& 1` gives us the least significant bit.
<!--SR:2022-09-27,85,250-->

## Variables and Mutability

What are variables?
?
Identifiers that hold non-signal data and are mutable.
<!--SR:2022-09-10,65,210-->

How do we declare a variable?
?
`var x;` declares a variable called `x`.
<!--SR:2022-09-09,74,250-->

What values do variables hold?
?
Values of the field, or arithmetic expressions (when used to generate constraints)
<!--SR:2022-09-18,57,170-->

What are the various ways we can assign to a variable?
?
```
var x;
x = 1;
var y = 2;
var z[3] = [3,4,5];
```
<!--SR:2022-08-05,47,230-->

What is wrong with the following code?
```
a = (b = 3) + 2;
```
?
An assignment, which is a statement and has no value, is being used as part of an expression. This is a compiler error.
<!--SR:2022-10-25,100,250-->

What is wrong with the following code?
```
var x;
if (x = 3) {
	var y = 0;
}
```
?
An assignment, which is a statement and has no value, is being used as part of an expression. This is a compiler error.
<!--SR:2022-07-29,44,230-->

# Templates

## Templates and Components

### Templates

What do we use to create generic circuits in circom?
?
Templates.
<!--SR:2022-09-26,84,250-->

When are template's parameters instantiated?
?
When the template is used.
<!--SR:2022-09-23,73,230-->

What is the syntax to define a template parameter?
?
```
template tempid (param_1, param2) {
	...
}
```
<!--SR:2022-09-01,66,250-->

What can templates not include?
?
Local functions or template definitions.
<!--SR:2022-07-26,44,250-->

What is wrong with the following code, and what error will it generate?
```
template wrong() {
	signal input a:
	signal output b;
	a <== N;
}
```
?
We are assigning a value to an input signal in the same template where it has been defined. The error will be "Exception caused by invald assignment."
<!--SR:2022-08-15,31,170-->

What is the syntax to instantiate template parameters?
?
`component c = tempid(value_1, ... , value_n)`;
<!--SR:2022-09-03,68,250-->

How are the possible values of template parameters restricted?
?
They should be known constants at compile time.
<!--SR:2022-08-26,60,250-->

What is wrong with the following code, and what error does it generate?
```
pragma circom 2.0.0;
template A(N1, N2) {
	signal input in;
	signal output out;
	out <== N1 * in * N2;
}
template wrong(N) {
	signal input a;
	signal output b;
	component c = A(a, N);
}
component main{public [a]} = wrong(1);
```
?
`A(a, N)` passes a signal to a template as a parameter, which means the value of the parameter can't be known at compile time.
"Every component instantiation must be resolved during the constraint generation phase."
<!--SR:2022-08-11,21,210-->

When do we use `--inspect`?
?
In the compilation phase.
<!--SR:2022-08-24,38,230-->

What is wrong with the following code and what error will it generate?
```
pragma circom 2.0.0;
template A(N) {
	signal input in;
	signal intermediate;
	signal output out;
	intermediate <== 1;
	out <== intermediate;
}
component main{public [in]} = A(1);
```
?
The `in` signal is not used in any constraints. 
It will give a warning when `--inspect` is used to compile: "In template "A1". Unconstrained signal. "in" = Maybe use: in*0 === 0"
<!--SR:2022-07-30,45,230-->

What is wrong with the following code and what error will it generate?
```
pragma circom 2.0.0;
template A(N) {
	signal input in;
	signal inter;
	signal output out;
	inter <== 1;
	out <== in;
}
component main{public [in]} = A(1);
```
?
The intermediate signal `inter` is only used in one constraint, which makes it effectively useless, as it can't constrain inputs to outputs.
It will give a hint when using `--inspect` at compile time: "In template "A1". One constraint intermediate: "inter" = Maybe use: inter * 0 === 0".
<!--SR:2022-09-27,72,210-->

What is wrong with the following code and what error will it generate?
```
pragma circom 2.0.0;
template A(N) {
	signal input in;
}
component main{public [in]} = A(1);
```
?
There is no output signal from the `A` template..
The warning at compile time with `--inspect` is: "There is no output signal"
<!--SR:2022-11-10,108,230-->

What, roughly, are the three compiler warnings you can get from misusing signals in a template?
?
Unconstrained signal.
Intermediary signal used in one constraint.
No output signal in template.
<!--SR:2022-09-14,59,190-->

### Components

What does a component represent?
?
An arithmetic circuit.
<!--SR:2022-11-03,105,250-->

What does a component consist of?
?
$N$ input signals, $M$ output signals, and $K$ intermediate signals.
<!--SR:2022-08-21,61,250-->

What can a component produce?
?
A set of arithmetic constraints.
<!--SR:2022-11-16,114,250-->

How do we access the input or output signals of a component?
?
Dot notation:
```
c.a <== y*z-1;
var x;
x = c.b;
```
<!--SR:2022-10-01,87,250-->

What is the difference between component instantiation and the component creation instruction? Why does it matter?
?
Instantiation won't be triggered until all the component's inputs have been supplied, meaning instantiaion may be delayed. This means the outputs of a component can't be used until all the inputs are set.
<!--SR:2022-09-22,80,250-->

What is wrong with the following piece of code?
```
pragma circom 2.0.0;
template Internal() {
	signal input in[2];
	signal output out;
	out <== in[0] * in[1];
}
template Main() {
	signal input in[2];
	signal output out;
	component c = Internal();
	inter.in[0] <== in[0]
	out <== c.out
	c.in[1] <== in[1]
}
component main{public[in]} = Main();
```
?
`c`'s output is accessed before one of its inputs.
<!--SR:2022-07-26,44,250-->

What's wrong with the following code and what error message does it produce?
```
component a;
if (N > 0) {
	a = A();
} else {
	a = B();
}
```
?
If there are multiple initialization instructions for a component, they must all be from the same template (perhaps with different parameters).
"Assignee and assigned types do not match"
<!--SR:2022-08-09,50,230-->

How do you make an array of components? What is the syntactic restriction?
?
You must initialize each component separately, for example:
```
component ands[2];
...
ands[0] = MultiAnd(n1);
ands[1] = MultiAnd(n2);
```
<!--SR:2022-08-08,42,230-->

When can we use `parallel`?
?
When components are independent, i.e., the inputs do not depend on each others' outputs.
<!--SR:2022-09-05,70,250-->

How do we use `parallel`?
?
`template parallel NameTemplate(...){...}`
<!--SR:2022-09-02,67,250-->

What does `parallel` do?
?
The C++ file resulting from compilation will contain parallelized code to compute the witness.
<!--SR:2022-09-04,69,250-->

When is parallelization particularly useful?
?
When dealing with large circuits.
<!--SR:2022-10-03,89,250-->




## Pragma

What is the line at the top of every circom file?
?
`pragma circom 2.0.0;`
<!--SR:2022-10-05,83,230-->

What is pragma for?
?
To ensure that the circuit is compatible with the specified compiler version.
<!--SR:2022-09-28,85,250-->

If there is no pragma, what do we assume?
?
That the code is compatible with the compiler's latest version.
<!--SR:2022-08-06,49,250-->

## Functions

What do functions do?
?
Define abstract pieces of code that can perform some computation to obtain a value or an expression to be returned.
<!--SR:2022-10-10,85,230-->

What does a function look like?
?
```
function funid (param_1, ..., param_n) {
	...
	return x;
}
```
<!--SR:2022-09-16,77,250-->

What can functions output?
?
Numeric values, or expressions, or arrays of one or the other.
<!--SR:2022-11-16,118,250-->

Can functions be recursive?
?
Yes.
<!--SR:2022-08-28,62,250-->

How many return statements can a function have?
?
As many as it likes.
<!--SR:2022-09-30,87,250-->

When is a return statement required?
?
At the end of every execution trace.
<!--SR:2022-09-05,69,250-->

What does executing a return statement do?
?
Returns control to the caller of the function.
<!--SR:2022-09-25,82,250-->

What error does this code produce?
```
function example(N) {
	if (N > 2) {
		return 0;
	}
}
```
?
"In example there are paths without return"
<!--SR:2022-10-02,88,250-->

## Include

How do you include library code?
?
`include "example_library.circom";`
<!--SR:2022-09-14,71,250-->

## The main Component

Where do we start execution?
?
The main component.
<!--SR:2022-09-30,87,250-->

How is the main component different from other components?
?
It defines global input and outputs of the circuit, so it needs to be able to specify which input signals are public.
<!--SR:2022-09-07,72,250-->

What is the syntax for creating a main component?
?
`component main{public [signal_list]]} = template_id(v1, ..., vn);` where `{public [signal_list]}` is optional.
<!--SR:2022-12-21,151,270-->

Which input signals in the main component are private?
?
All input signals not explicitly declared to be public.
<!--SR:2022-09-14,76,250-->

How can we define multiple main components in one program?
?
We can't - we'll get a "Multiple main components  in the project structure" error.
<!--SR:2022-09-25,83,250-->



# Syntax

What is the comment syntax for circom?
?
`//` for single line, and `/**/` for multiline.
<!--SR:2022-09-26,83,250-->

What can be used for identifiers?
?
`*[a-zA-Z0-9_$]`
<!--SR:2022-08-12,53,250-->

What are the reserved keywords?
?
signal
input
output
public
template
component
var
function
return
if
else
for
while
do
log
assert
include
pragma circom
<!--SR:2022-08-08,18,130-->

# Operators

What, roughly, is the operator precedence?
?
Conditional
Arithmetic
Bitwise
Relational
Logical
Assignment
<!--SR:2022-08-20,40,170-->

Where can operators be used?
?
To make expressions, but the conditional operator can only be used at the top level.
<!--SR:2022-09-07,68,250-->

What are the possible values of a field element?
?
It's in the domain `Z/pZ`, where p is a prime number, defaulting to a particular large number.
<!--SR:2022-10-04,89,250-->

What do you use to change the field size?
?
`GLOBAL_FIELD_P`
<!--SR:2022-11-11,116,250-->

What is the conditional expression?
?
`_?_:_`
<!--SR:2022-08-11,52,250-->

What are the boolean operators?
?
`&& || !`
<!--SR:2022-09-11,73,250-->

What is `&&`?
?
Boolean AND operator.
<!--SR:2022-09-17,74,250-->

What is `||`?
?
Boolean OR operator.
<!--SR:2022-08-20,58,250-->

What is `!`?
?
Boolean NEGATION operator.
<!--SR:2022-09-10,73,250-->

What are the relational operators?
?
`< > <= >= == !=`
<!--SR:2022-11-17,120,250-->

What is the `val(x)` function for?
?
Defining negative numbers for use with the relational operators.
<!--SR:2022-09-05,66,250-->

What is the definition of the `val(x)` function?
?
```
val(z) = z - p if p/2 + 1 <= z < p
val(z) = z, otherwise
```
<!--SR:2022-09-05,42,230-->

How is `x < y` defined?
?
`val(x % p) < val(y % p)`
<!--SR:2022-09-03,65,250-->

How is `x > y` defined?
?
`val(x % p) > val(y % p)`
<!--SR:2022-09-24,81,250-->

How is `x <= y` defined?
?
`val(x % p) <= val(y % p)`
<!--SR:2022-10-07,88,250-->

How is `x >= y` defined?
?
`val(x % p) >= val(y % p)`
<!--SR:2022-11-20,121,250-->

What are the arithmetic operators?
?
`+ - * ** / \ %`
<!--SR:2022-09-21,79,250-->

What are the `+ - * **` operators?
?
Addition, subtraction, multiplication, exponentiation all mod p.
<!--SR:2022-10-04,89,250-->

What is the `/` operator?
?
Multiplication by the multiplicative inverse mod p.
<!--SR:2022-09-19,67,210-->

What is the `\` operator?
?
Quotient after integer devision.
<!--SR:2022-12-23,151,270-->

What is the `%` operator?
?
Remainder after integer division.
<!--SR:2022-08-09,48,230-->

What are the arithmetic/assignment operators?
?
`+= -= *= **= /= \= %= ++ --`
<!--SR:2022-11-29,130,250-->

What are the bitwise operators?
?
`& | ~ ^ >> <<`
<!--SR:2022-09-10,53,250-->

What is the `&` operator?
?
Bitwise AND
<!--SR:2022-09-15,72,250-->

What is the `|` operator?
?
Bitwise OR
<!--SR:2022-09-27,84,250-->

What is the `~` operator?
?
Complement 254 bits
<!--SR:2022-09-12,57,210-->

What is the `^` operator?
?
XOR 254 bits
<!--SR:2022-09-15,57,190-->

What is the `>>` operator?
?
Rightshift
<!--SR:2022-10-05,89,250-->

What is the `<<`?
?
Leftshift
<!--SR:2022-08-27,61,250-->

How are the shift operators extended?
?
They work modulo p (assuming p>=7).
<!--SR:2022-09-26,76,230-->

How do the shift operators work for `0 >= k <= p/2`?
?
```
x >> k = x/(2**k)
x << k = (x*(2{**}k)~ & ~mask) % p
```
where b is the number of significant bits of p and mask is `2{**}b - 1`
<!--SR:2022-09-21,64,190-->

How do the shift operators work for `p/2 + 1 <= k < p`?
?
```
x >> k = x << (p - k)
x << k = x >> (p - k)
```
<!--SR:2022-08-04,12,150-->

What are the bitwise assignment operators?
?
`&= |= ~= ^= >>= <<=`
<!--SR:2022-09-29,85,250-->

What is the code for the `IsZero` template?
?
```
pragma circom 2.0.0;
template IsZero() {
	signal input in;
	signal output out;
	signal inv;
	inv <-- in!=0 ? 1/in : 0;
	out <== -inv*in +1;
	in*out === 0;
}
component main{public [in]} = IsZero();
```
<!--SR:2022-08-18,51,230-->

What is the code for `Num2Bits`
?
```
pragma circom 2.0.0;
template Num2Bits(N) {
	signal input in;
	signal output out[N];
	var lc1=0;
	var e2 = 1;
	for (var i = 0; i < N; i++) {
		out[i] <-- (in >> i) & 1;
		out[i] * (out[i] - 1) === 0;
		lc1 += out[i] * e2;
		e2 = e2 + e2;
	}
	lc1 === in;
}
component main{public[in]} = Num2Bits(3);
```
<!--SR:2022-08-03,45,230-->

# Constraint Generation

What is a linear expression?
?
An expression where only addition is used.
<!--SR:2022-10-02,87,250-->

How can we rewrite some linear expressions succinctly?
?
By multiplying variables by constants, i.e., `2*x` is equivalent to `x+x`.
<!--SR:2022-07-31,41,230-->

What is a quadratic expression?
?
An expression resulting from the multiplication of two linear expressions and addition of another: `A*B+C` where `A,B,C` are linear expressions.
<!--SR:2022-09-30,85,250-->

Circom generates constraints, what form must they have?
?
They must be quadratic of the form `A*B+C=0` where `A,B,C` are linear combinations of variables.
<!--SR:2022-09-28,84,250-->

What transformations does circom apply to correctly form constraints?
?
Moves from one side of the equality to the other.
Applications of the commutativity of addition.
Multiplication (or division) by constants.
<!--SR:2022-07-28,31,230-->

Which operators impose constraints?
?
`===`, `<==`
<!--SR:2022-10-04,89,250-->

Rewrite `out <== 1 - a * b;` more explicitly
?
```
out === 1 - a * b;
out <-- 1 - a * b;
```
<!--SR:2022-08-14,54,250-->

What kinds of expressions are allowed in constraints?
?
Quadratic expressions.
<!--SR:2022-08-08,50,250-->

What is wrong with the following code and what error does it produce?
```
template multi3() {
	signal input in;
	signal input in1;
	signal input in2;
	signal output out;
	out <== in*in1*in2;
}
```
?
The constraint `out === in*in1*in2` is not quadratic so we get:
"Non quadratic constraints are not allowed!"
<!--SR:2022-09-19,76,250-->

Write out the full constraint generated by the following code, why does it work like this?
```
signal input a;
signal output b;
x = a * a;
b <== x + 3;
```
?
`b === a * a + 3`
Because `x` holds the algebraic expression `a*a` which is used to generate constraints over signals, because we can't use variables in a constraint.
<!--SR:2022-09-18,75,250-->

# Control Flow

What control flow constructions do we have?
?
`if`, `for`, and `while`
<!--SR:2022-11-08,106,250-->

What is the syntax `if` statements?
?
`if ( boolean_condition ) block_of_code else block_of_code`
The else block is optional.
<!--SR:2022-10-27,94,230-->

What is the syntax for `for` loops?
?
`for ( initialization_code ; boolean_condition ; step_code ) block_of_code`
<!--SR:2022-08-30,64,250-->

What's wrong with the following code?
```
var y = 0;
for(var i = 0; i < 100; i++){
	y++;
}
i++
```
?
`i` is only in scope for the `for` block and can't be used outside of it.
<!--SR:2022-09-06,70,250-->

What is the syntax for a `while` loop?
?
`while ( boolean_condition ) block_of_code`
<!--SR:2022-12-02,137,270-->

What restriction is placed on constraints inside control flow blocks?
?
The conditions of the flow control blocks cannot be unknown. This is because constraint generation must be unique and cannot depend on unknown input signals.
<!--SR:2022-08-16,55,250-->

What is wrong with the following code?
```
pragma circom 2.0.0;
template A(){}
template wrong(N1){
	signal input in;
	component c;
	if (in < N1) {
		c = A();
	}
}
component main{public [in]} = wrong(1);
```
?
The condition depends on an unknown, and there are constraints generated inside the condition. This makes it impossible to generate a static circuit from the code.
<!--SR:2022-08-31,65,250-->

What template has an error and why?
```
template A(N){
	signal input in;
	component c;
	if (in < N) {
		c = SomeC()
	}
}
template B(N1, N2) {
	signal input in;
	var x = 2;
	var x = 5;
	if (N1 > N2) {
		t = 2;
	}
	x === 2;
}
```
?
`A`, because its condition depends on a signal which means it's unknown, whereas `B`'s depends on a parameter which means it's known at compile time.
<!--SR:2022-10-05,89,250-->

What is wrong with the following code?
```
template wrong() {
	signal input in;
	var x;
	var t = 5;
	if (in < 3) {
		t = 2;
	}
	x === t;
}
```
?
The value of `t` is used in a constraint and its construction depends on the unknown signal `in` via control flow, making the resulting constraint non quadratic. This will cause a compiler error.
<!--SR:2022-09-12,74,250-->

# Data Types

What are the basic var types?
?
Field elements and arrays.
<!--SR:2022-11-30,128,250-->

What is the default type of signals and variables?
?
A field element.
<!--SR:2022-09-04,68,250-->

Are arrays dynamic?
?
No, they can hold a finite number of elements known at compile time.
<!--SR:2022-09-15,76,250-->

How many different types of elements can a single array hold?
?
Just one type.
<!--SR:2022-09-02,66,250-->

What types can arrays hold?
?
Signals, vars, the same type of component, or arrays.
<!--SR:2022-08-17,51,230-->

How, for example, do we declare a 2D array with lengths?
?
`var dbl[16][2];`
<!--SR:2022-08-29,63,250-->

What is wrong with the following code?
`var z = [2,8,4];`
?
The size of `z` is not explicitly given, and it will produce a compiler error.
<!--SR:2022-10-03,88,250-->

Can a single array hold multiple types of signals?
?
No, each array can only hold one type of signal.
<!--SR:2022-09-20,78,250-->

Can an array contain components with different parameters?
?
Yes, as long as they have the same type.
<!--SR:2022-10-05,89,250-->

What is wrong with the following code and what error message will it give?
```
pragma circom 2.0.0;
template fun(N){
	signal output out;
	out <== N;
}
template fun2(N){
	signal output out;
	out <== N;
}
template All(N){
	component c[N];
	for (var i = 0; i < N; i++) {
		if (i < N){
			c[i] = fun(i);
		} else {
			c[i] = fun2(2);
		}
	}
}
```
?
`c[i] = fun[i] -> Assignee and assigned types do not match`
There are two types of components being put into the array `c`. This applies even though the two types are identical, and no components can actually be of type 2 if you follow the runtime logic.
<!--SR:2022-09-27,81,250-->

# Scoping

How does scoping work?
?
We have static/lexical scoping, and that signals must be defined at the top level block of the template that uses them, effectively giving them global scope.
<!--SR:2022-08-31,65,250-->

What is wrong with the following code and what error does it produce?
```
pragma circom 2.0.0;
template Multiplier2(N){
	signal input in;
	signal output out;
	
	out <== in;
	signal input x;
	if (N > 0) {
		signal output out2;
		out2 <== x;
	}
}
component main{public [in]} = Multiplier2(5);
```
?
The `out2` signal is declared inside a nested block.
"`out2` is outside the initial scope".
<!--SR:2022-08-15,46,230-->

Which signals of subcomponents are visible?
?
The direct children's signals are visible, but none of their descendant's signals are visible.
<!--SR:2022-08-01,41,230-->

What is wrong with this code?
```
template d() {
	signal output x;
	x <== 1;
}
template c() {
	signal output out2;
	out2 <== 2;
	component comp2 = d();
}
template t() {
	signal output out;
	component c3 = c();
	out <== c3.comp2.x;
}
```
?
`t` is trying to access a component within a component which is not allowed. If we want an indirect descendant's signals, we need to pass them via the intervening components.
<!--SR:2022-09-24,80,250-->









# Code Quality

What does assert do?
?
Introduces a condition to be checked at execution time. If the condition fails, the witness generation is interrupted and the error is reported.
<!--SR:2022-08-17,36,170-->

What creates assertions?
?
The `assert` keyword, and constraints.
<!--SR:2022-08-02,45,230-->

How do you use `assert`, for example?
?
`assert(n <= 254);`
<!--SR:2022-10-01,86,250-->

What is `log`?
?
A way to log values to the standard error stream.
<!--SR:2022-08-15,55,250-->

What can be passed to `log`?
?
Any expression except the conditional expression.
<!--SR:2022-08-12,18,230-->

What's an example of a `log` instruction?
?
`log(123);`
<!--SR:2022-10-21,94,250-->

# Circom Insights
## Compiler

What are the compiler phases called and what do they do?
?
Construction, where constraints are generated
Code generation, where the code to compute the witness is generated
<!--SR:2022-07-29,32,230-->

What kinds of compiler messages are there?
?
Hints, warnings, and errors.
<!--SR:2022-10-01,85,250-->

What is a hint?
?
A compiler message that means that what you've done is allowed but uncommon, so it's better to check if it was done on purpose.
<!--SR:2022-10-12,92,250-->

What is a warning?
?
A compiler message meaning that what you've done is allowed but should not happen in general.
<!--SR:2022-09-09,72,250-->

 ??? why do we suggest adding a `0*in = 0` signal where `in` is unused? Surely we should just get rid of `in`, or at least leave it, as the constraint does nothing but add code.

What is an error?
?
A compiler message meaning that what you've done is not allowed, and the compilation of the program fails.
<!--SR:2022-10-13,92,250-->

What is wrong with the following code, and what message is genreated?
```
template A() {
	signal x;
	x = 1;
	signal out <== x;
}
```
?
You can't assign to a signal using `=`.
An error message saying that "Assignee and assigned types do not match operator."
<!--SR:2022-08-06,25,210-->

## Unknowns

Why are checks imposed on the use of unknown values at compile?
?
Because expressions accepted during constraint generation have to be quadratic.
<!--SR:2022-09-04,55,230-->

What kinds of values are always known or unknown?
?
Constant values and template parameters are known.
Signals are unknown.
<!--SR:2022-09-08,71,250-->

When are expressions known?
?
Expressions depending on only known values are known.
Expressions depending on unknowns are unknown.
<!--SR:2022-10-10,90,250-->

Which identifiers and known and unknown in the following code?
```
template A(n1, n2) {
	signal input in1;
	signal input in2;
	var x = 0;
	var y = n1;
	var z = in1;
}
```
?
`n1`, `n2`, `x`, and `y` are known.
`in1`, `in2`, and `z` are unknown.
<!--SR:2022-10-23,110,270-->

A constraint with an array access . . . ?
?
Must have a known accessing position.
<!--SR:2022-08-01,46,250-->

What is wrong with the following code, and what message does it generate?
```
template A(n) {
	signal input in;
	signal output out;
	var array[n];	
	out <== array[in];
}
```
?
The index for the array in the constraint is unknown.
"Error: Non-quadratic constraint was detected statically, using unknown index will cause the constraint to be non-quadratic"
<!--SR:2022-08-04,48,250-->

What restrictions are placed on the size of an array?
?
The size must be a known value.
<!--SR:2022-08-19,58,250-->

What is wrong with the following code and what message does it generate?
```
template A() {
	signal in;
	var array[in];
}
```
?
Length of `array` must be known.
"Error: The length of every array must known during the constraint generation phase"
<!--SR:2022-10-09,89,250-->

A control flow with a constraint . . . ?
?
Must have a known condition.
<!--SR:2022-08-07,50,250-->

What is wrong with the following code and what message does it generate?
```
template A() {
	signal input in;
	signal output out;
	if (in < 0) {
		out <== 0;
	}
}
```
?
There is a constraint in control flow with an unknown condition.
"Error: There are constraints depending on the value of the condition and it can be unknown during the constraint generation phase"
<!--SR:2022-08-29,63,250-->

What two things are wrong with the following code and what message does it generate?
```
template A() {
	signal input in;
	signal output out;
	for (var i = 0; i < in; i++) {
		out <== i;
	}
}
```
?
There is a constraint in control flow with an unknown condition.
"Error: There are constraints depending on the value of the condition and it can be unknown during the constraint generation phase"
Also, out is assigned multiple times.
<!--SR:2022-07-28,41,230-->







