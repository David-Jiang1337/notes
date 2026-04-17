# Matrices as Functions
Informally, we can understand matrix multiplication with a matrix $A$ and a vector $x$ as a function that takes an $x$ as input and produces a vector $b$ as output. As such, $x$ is our independent variable that we vary, and $b = Ax$ is our dependent variable that changes depending on $x$. The input and output vectors need not be of the same dimensions. In fact, they are the same dimension if and only if $A$ is a square matrix, as for any $m \times n$ matrix $A$,
- The input vector $x$ is in $R^n$
- and the output vector $b = Ax$ is in $R^m$. 
The set of all possible outputs $b$ is equal to the column space $Col(A)$, as the equation $Ax = b$ can only be consistent where $b$ is in the span of the columns of $A$.

# Transformations
A linear transformation as we should call them, is a function between vector spaces, taking members of one member space and turning it into the members of another vector space (i.e. $R^n \to R^m$). We say that a transformation $T$ of $R^n$ to $R^m$ is a rule that takes a vector $x \in R^n$ and turns in into a vector $T(x) \in R^m$. As such, $R^n$ is the domain of $T$, and $R^m$ is the codomain of $T$. Specifically, we do not call the vector $T(x)$ an output vector, but instead say that $T(x)$ is the **image** of $x$ under $T$. The set of all images $\{T(x) | x\ \in R^n \}$ is the **range** of $T$, just like in functions the set of $\{f(x)| x \in R\}$ is the range of $f$.

## The Identity Transformation
The identity transformation is possibly the simplest transformations we could devise, as this transformation $Id_n$ with a domain and codomain of $R^n$ simply takes in a vector $x \in R^n$ and spits it back out. Formally:
$$Id_n(x) = x, x\in R^n$$
The matrix that we use for such a function is the $n \times n$ identity matrix, i.e. a $n \times n$ matrix where all diagonal values are $1$ and all other values are $0$.

## Matrix Transformations
As MATH 221 is about matrices and linear algebra, we can specialize the concept of transformations to obtain the concept of matrix transformations, that is, a subset of transformations such that the matrix transformation $T$ can be expressed as $T(x) = Ax$ of a $m \times n$ matrix $A$ and a vector $x \in R^n$ where $T(x) \in R^m$. Again, remember that the range of $T$ is the column space $Col(A)$.