---
title: Diffeq
date: 2025-01-27T14:39:33-05:00
draft: false
---
I'm ASEing diffeq this IAP. The test is tomorrow, I'm finishing up the final sections of the homework packet. I don't have too much time before 8.20 lecture today, so I'll instead do a little review:

## how fast are you going?
basically with diffeq we're trying to solve equations that relate how fast you're going (and acceleration, and higher orders) with the function itself. most of the diffeqs we are able to solve are of the form
$$ \sum a_n(x) y^{(n)} = f(x) $$
which is linear in y, so we call it a *linear differential equation*. 

the main things to know are (1) how to solve for a general, *homogenous* solution (i.e. imagine $f(x)=0$), (2) how to find a *particular* solution, and (3) how to visualize the solutions to an equation without solving for it if you can't do (1) and (2), especially when the coefficients $a_n$ aren't constant. Also, know how to do this for systems of diffeqs, with matrices.

why are (1) and (2) separate? there are many solutions $y_i$ to a diffeq (without initial values), related by the fact that $y_i - y_j$ is a solution to the homogenous diffeq. So we just need to find a single particular solution to a diffeq, and then add any linear combination of solutions for the homogenous diffeq to get the full set of solutions to the equation.

we proceed to outline how to find solutions (1),(2) in the case where $a_n$ are constant.
## homogenous solution
imagine that $f(x)$ is 0, and then solve. do this by guessing $y = e^{rx}$, so after substituting into the equation and dividing by $y$ you get $\sum a_n r^n = 0$, the *characteristic equation*. Solve this equation to get all the possible $r$, and a linear combination of the independent functions $e^{rt}$ gives you the general solution. for a repeated root $s$ of multiplicity k, the corresponding independent functions are $s^j e^{st}$ for all $0 \leq j < k$.

If the characteristic equation has complex roots, note that $c_1e^{a + bi} + c_2 e^{a - bi} = e^a (d_1 \cos(z) + d_2 \sin(z))$ through a linear transformation of coefficients $c_1 = (d_1 + d_2/i)/2$ and $c_2 = (d_1 - d_2/i)/2$, so you can use $e^{at} \cos(bt)$ and $e^{at} \sin(bt)$ for which you can find real coefficients $d_1, d_2$. (otherwise you will need some restrictions on $c_1, c_2$ if you use the complex exponentials in a basis for your real solution $y$.)
## particular solution
goal: we want a $y$ such that $$ \sum a_n y^{(n)} = f(x) $$
therefore we want a $y$ such that $f(x)$ is a particular linear combination of it and its derivatives. then if $f(x)$ is a polynomial of degree $k$ in $x$, we can guess a particular solution for $y$, call it $y_p$, is also a polynomial of degree $k$, so that taking a linear combination of derivatives of $y_p$ in the LHS is also a polynomial of degree $k$ in $x$, just like $f(x$). then equating coefficients will give us $k$ equations to solve for the $k$ coefficients in $y_p$. if the equations have multiple solutions, we only need one, as we can get the rest from adding the general homogenous solution.

similarly, if $f(x)$ is some linear combination of $\sin(ax)$ and $\cos(ax)$, we know that the derivatives of these are also linear combinations of $\sin(ax)$ and $\cos(ax)$, so we guess $y_p$ as such a linear combination, so that plugging in gives us a linear combination of these functions on the LHS, just like $f(x)$, and equating coefficients gives us 2 equations for the 2 variables. see the pattern? (it's reasonably called the method of *undetermined coefficients*.) the last case is when $f(x)$ is a constant times $e^{ax}$, in which case we guess $f(x)$ is of the same form. notice that the sine and cosine case reduces to the exponential case by representing them with complex exponentials.

obviously, we can find a particular solution where $f(x)$ is a linear combination of functions $\sum a_i g_i(x)$ that fit in these three cases by finding particular solutions $y_{p,i}$ where the RHS is each $g_i$, and then taking $\sum a_i y_{p,i}$ to be a particular solution to when the RHS is $f(x)$. this is because the differentiation operator is linear. less obviously a function that is any product of the cases is also solvable using the same principle of guessing $y_p$ such that $f(x)$ can be represented as a linear combination of $n$ derivatives of $y_p$. 

something i overlooked is... what if the form we choose for $y_p$ is a solution to the homogenous equation? then $\sum a_n y_p^{(n)}$ is $0 \neq f(x)$. in this case, we just multiply our initial guess for $y_p$ by $x$ until it no longer becomes a solution to the homogenous equation. we can see this works by noting $f(x)$ must then be a linear combination of exponentials or a power of $x$ times an exponential, so we just take one at a time, say $g_i(x) = x^t e^{rx}$. Then $r$ must be an $s$-fold root of the characteristic equation $p$ (where $s > t$), where $p(D)y_p$ is the RHS, so that the equation can be can be written as $q(D)(D-r)^s y_p = g_i(x)$. Then do $(D-r)^t$ on both sides, so we get $q(D)(D-r)^{s+t}y_p = 0$, so $y_p$ must be a solution to this homogenous equation. However, it cannot be a solution to the original $p(D)y = 0$, as we've seen. So it must be a linear combination of powers of $x$ times $e^{rx}$; in particular the powers $m$ of $x$ must be at least $s$ so that $x^m e^{rx}$ is not a solution to $p(D)y = 0$. Therefore our particular solution $y_p$ for $p(D)y = \sum a_n y^{(n)} = g_i(x) = x^t e^{rx}$ will consist of a linear combination of terms $x^m e^{rx}$ where $s \leq m < s+t$. 

## systems of equations
You can turn any system of higher-order differential equations to a system of first order of differential equations by introducing more variables for every higher order (other than the highest order, of course). if this is a linear homogenous system, you can represent it a a matrix $\mathbf{x}' = A\mathbf{x}$ where A is a constant matrix. Then you can guess normal modes $\mathbf{x} = e^{\lambda t} \mathbf{v}$, and plugging it in tells you $\mathbf{v}$ must be an eigenvector with $\lambda$ as an eigenvalue. finding all of the eigenvectors and corresponding eigenvalues gives you all of the normal modes, and you can take a linear combination of these to get the general solution. for complex eigenvalues, you can get real basis functions instead by taking the real and complex parts of $e^{\lambda t} v$. for repeated eigenvalues $\lambda$ of multiplicity $k$, the good ("complete") case is when the there are $k$ distinct eigenvectors, but for 2 dimensions the matrix would just be $$\begin{bmatrix}  
\lambda & 0 \\  
0 & \lambda 
\end{bmatrix}$$which is generally not the case, and if it was you'd know it well beforehand. instead, for 2 dimensions, use a linear combination $\mathbf{z} = (\vec{\beta} + \vec{\alpha}t)e^t$ where $\vec{\alpha}$ is the eigenvector you found, and $\vec{\beta}$ is a solution to $(A - \lambda I) \vec{\beta} = \vec{\alpha}$ (which you can verify by plugging $\mathbf{z}$ in to the original system $\mathbf{x}' = A \mathbf{x}$ yourself). since $(A - \lambda I)$ is singular (for the 2d case), this system must be solved by elimination, without inverses. for higher dimensional cases, the general solution essentially tacks on more powers of $t$ as usual. see [this](https://www.math.purdue.edu/~neptamin/303Au21/Handouts/High_defect.pdf) pdf for more details... but...

it may be simpler to just "flatten" the $n$-dimensional system into an $n$-th order linear diffeq and solve it using its characteristic equation. this is done by eliminating any variable $x_i$ by writing it as a linear combination of the other dimensions and their derivatives, and then thereby writing $\dot{x_i}$ as a derivative of said linear combination, which is a linear combination of one higher order. rinse and repeat until you only have one variable. this process called *elimination*, but i like "flatten" better.

if you can change bases to one where you get a diagonal matrix, can write $A = S^{-1}\Lambda S$. then solution is 
$$S^{-1}\begin{bmatrix}  
e^\lambda_1 & 0 \\  
0 & e^\lambda_2 
\end{bmatrix} S$$
which we define to be $e^{At}$, as the definition for that is "$e^{At}\mathbf{x(0)}$ is a solution to $\mathbf{x}' = A\mathbf{x}$". S is a matrix that has eigenvectors of A as columns. doing a change of basis makes the evolution of variables very easy to compute/visualize!
## i can't solve it...
no worries, differential equations are not all solvable! there are a couple of methods that you can use to figure out how it generally looks, depending on your resources and needs.

1. use a computer
	1. what does a computer use though?
		2. a variant of euler's method (original: find $x(x_0+\epsilon)$ using derivative at $x_0$, which gives you more accuracy as $\epsilon$ decreases, until rounding errors overtake and suddenly you get less accuracy because they accumulate faster as $\epsilon$ decreases)
			1. variant basically finds a guess for $x(x_0 + \epsilon)$ using $x'(x_0)$ (call the guess $g$), but actually set $x(x_0 + \epsilon)$ using average of derivatives $x'(x_0)$ and $x'(g)$. we get much better accuracy for the same epsilon using this method compared to regular euler
	2. euler's method is good for when you want precision for a particular trajectory
	3. i've only outlined the case where $x' = f(x)$, but works for any first-order ODE $x' = f(x,t)$ as well of course, just increment $t$ instead of $x$ directly
2. what if you want to visualize things without as much computation power
	1. first-order ODE $y' = f(x,y)$
		1. direction field: at various $(x,y)$ draw $y'$. easy to do by focusing on *isoclines*, curves where $f(x,y)$ is a constant, can draw the same slope $c$ along the entire curve
	2. 2d homogenous system $\mathbf{x'} = A\mathbf{x}$
		1. 9 different types of systems depending on trace and determinant of $A$
			1. node (real eigenvalues of same sign); can be stable or unstable
			2. saddle (real eigenvalues of different sign); always unstable
			3. spiral (complex eigenvalues with nonzero real part); can be stable or unstable
			4. center (only imaginary eigenvalues)
			5. comb (one eigenvalue is 0)
			6. star (complete repeated eigenvalue)
			7. degenerate node (repeated eigenvalue, not complete)

## conclusion
exponential functions are really cool! in fact, $e^x$ was basically defined to be really cool (solution of $y' = y$)!

## resources
material for the hw packets mostly come from https://math.mit.edu/~jorloff/suppnotes/suppnotes03/ASENotesAndExercises.html and chapters 1,2,8 of Edwards and Penney, Elementary Differential Equations with Boundary-Value Problem, 6th edition, Prentice-Hall.