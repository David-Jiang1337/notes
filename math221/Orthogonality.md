Orthogonality is the generalization of perpendicularity to dimensions $R^n$ such that $n > 3$. In spaces $R^2$ and $R^3$, we can clearly visualize orthogonality. In $R^2$, given any vector $v_1$, we can intuitively see that any vector $v_2$ perpendicular (orthogonal) to $v_1$ has no component in the direction of $v1$. Likewise, we can see in $R^3$ that given two vectors $v_1, v_2$, a vector $v_3$ orthogonal to $v_1, v_2$ has no component in the directions of $v_1$ or $v_2$.

To formalize the concept of orthogonality beyond visual examination, we should first define a dot product.
# Dot Product
A dot product is an operation denoted with a dot "$\cdot$" that takes two vectors and produces a scalar representing the magnitude of the direction they have in common.
$$\displaylines{\text{for vectors }a = (a_1, a_2, a_3,...a_n) , b=(b_1, b_2, b_3,... b_n) \in R^n,\\ a \cdot b = a_1b_1 + a_2b_2 + a_3b_3 +... a_nb_n}$$
Dot products have the following properties for $a,b,c \in R^n, k \in R$
- **Commutativity**: $a \cdot b = b \cdot a$
- **Distributivity with Addition**: $c\cdot (a + b) = c\cdot a + c\cdot b$
- **Associativity with Scalar Multiplication**: $(ka)\cdot b = k(a\cdot b)$

We may note that for a vector $a = (a_1, a_2, a_3,... a_n) \in R^n$, $a \cdot a = a_1^2 + a_2^2 + a_3^2 + ... a_n^2$. This tells us two things:
- $\sqrt{a\cdot a} = ||a||$; the length of $a$ is the square root of $a \cdot a$
- $a \cdot a = 0 \iff a = 0$
We can further conclude from the dot product's associativity with scalar multiplication:
$$\displaylines{\text{for }x = (x_1, x_2, x_3,... x_n) \in R^n, c \in R\\ ||cx|| = |c| \cdot ||x||}$$
# Unit Vector
To reiterate from MATH 200, we know a unit vector $x \in R^n$ is a vector such that $||x|| = 1$. We can take any vector $y \in R^n$ and get a unit vector in the same direction by dividing $y$ by its length: $\frac{y}{||y||}$.
# Orthogonal Vectors
We represent two vectors $x,y \in R^n$ being orthogonal as $x \perp y$. Suppose $x = (x_1, x_2), y = (y_1, y_2) \in R^2$ are orthogonal. We would expect the angle between them to be $\theta = \frac{\pi}{2}$. We know from the law of cosines that: $$||y - x||^2 = ||x||^2 + ||y||^2 - 2||x||\cdot ||y||cos(\theta)$$
In the case $x \perp y$, $cos(\theta) = cos(\frac{\pi}{2}) = 0$, so:
$$x\perp y \iff ||y - x||^2 = ||x||^2 + ||y||^2$$
We can also simplify $||y - x||^2 = ||x||^2 + ||y||^2$ into $x \cdot y = 0$, so we get the definition of orthogonality: $$x\perp y \iff ||y - x||^2 = ||x||^2 + ||y||^2 \iff x\cdot y = 0$$
# Orthogonal Complement
Now that we know what an orthogonal vector is, we can derive a set of ALL vectors orthogonal to a subspace using the definition of orthogonal. We say that for a set of vectors $W$ that it a subspace of $R^n$, $W^\perp$ is the set of all vectors orthogonal to the vectors in $W$. Formally: $W^\perp = \{v \in R^n | \forall w \in W, v \cdot w = 0\}$.

Suppose we have a subspace $W$ of $R^3$ with two vectors  $w_1 = (w_{1,1}, w_{1,2}, w_{1,3}), w_2 = (w_{2,1}, w_{2,2}, w_{2,3})$. To check that a vector $x = (x_1, x_2, x_3)$ is orthogonal to $W$, we should see if $w_1 \cdot x = 0 \land w_2 \cdot x = 0$. Expanding our dot products by their definition, we get: $$\displaylines{w_{1,1}x_1 + w_{1,2}x_2 + w_{1,3} x_3 = 0 \\ w_{2,1}x_1 + w_{2,2}x_2 + w_{2,3} x_3 = 0}$$
We may notice that this is the exact definition of the null space of $W$, and indeed, it is true that for all subspaces $W$ of $R^n$, $W^\perp = Nul(W)$.

Using the above observations, we can derive some key properties of orthogonal complements for a subspace $W$ of $R^n$:
- $W^\perp$ is also a subspace of $R^n$
- $(W^\perp)^\perp = W$
- $\text{dim } W + \text{dim } W^\perp = n$

If we then conceptualize a $m \times n$ matrix $A$ as being $m$ rows of vectors with each vector being in $R^n$, it follows that the row space (i.e. the set of all linear combinations of these $m$ vectors in $R^n$) represents a subspace, and as we just established of subspaces, the null space of this matrix $A$ represents the subspace in which all vectors orthogonal to vectors in $A$ belong (i.e. $Row(A)^\perp = Nul(A)$).

Since transposition means mirroring the matrix so that its rows are now columns, we know that $Row(A^T) = Col(A)$. So $Col(A)^\perp = Row(A^T)^\perp = Nul(A^T)$.

Finally, we can use the periodicity of orthogonal complements to obtain these four statements:
- $Row(A)^\perp = Nul(A)$
- $Row(A) = Nul(A)^\perp$
- $Col(A)^\perp = Nul(A^T)$
- $Col(A) = Nul(A^T)^\perp$
## Row Rank and Column Rank Theorem
After deriving these facts about orthogonal complements, we can make an unexpected observation. Recall that the rank theorem states that the rank (i.e. the number of linearly independent vectors or the number of pivots) of a matrix $A$ plus the nullity of $A$ is equal to the number of columns in $A$. That is to say, for a $m \times n$ matrix $A$, $\text{dim } Col(A) + \text{dim } Nul(A) = n$. 
Using the equivalences we just derived, we can substitute $Nul(A)$ for $Row(A)^\perp$ , so $\text{dim } Col(A) + \text{dim } Row(A)^\perp = n$. 
We also know that $\text{dim } Row(A) + \text{dim } Row(A)^\perp = n$, so $\text{dim } Col(A) + \text{dim } Row(A)^\perp = \text{dim } Row(A) + \text{dim } Row(A)^\perp$
Subtracting $\text{dim } Row(A)^\perp$ from both sides, we get: $\text{dim } Col(A) = \text{dim } Row(A)$
That is, the dimensions of the column and row space of $A$ are the same for any matrix.

# Orthogonal Projection
An orthogonal projection of a point $x \in R^n$ onto a subspace $W$ of $R^n$ is the point $x_W \in W$ that is closest to $x$. We typically say that the orthogonal projection of $x$ onto $W$ is $x_W$

If we think about a $2$ dimensional space geometrically, we can intuitively tell that for any point $x$ and line $W$, drawing the shortest line from $x$ to a point $x_W$ which is on $W$ would necessarily mean drawing a line perpendicular to $W$ because of the Pythagorean theorem, as the distance $\sqrt{a^2 + b^2}$ would necessarily increase if we drew the line at a different angle than $\frac{\pi}{2}$. 

## Orthogonal Decomposition Theorem
The orthogonal decomposition theorem states that for a subspace $W$ of $R^n$ and a vector $x \in R^n$, there exists unique vectors $x_W \in W$ and $x_{W^\perp} \in W^\perp$ such that $x = x_W + x_{W^\perp}$. Formally:
$$\displaylines{\text{let }W \text{ be a subspace of } R^n\\ \forall x,\exists!x_w\in W,x_{W^\perp }\in W^\perp, x = x_W + x_{W^\perp}}$$
This makes sense intuitively in $R^2$ and $R^3$, where we can connect that point $x$ previously mentioned to the origin by drawing a perpendicular line  from $x$ to $x_W \in W$ and then drawing a line on $W$ from $x_W$ to $(0,0)$ or $(0,0,0)$ depending on the dimensions. 

Typically, we say that the orthogonal decomposition of $x$ with respect to $W$ is $x_W + x_{W^\perp}$.

## Computing Orthogonal Projections
For a given subspace represented by the span of some vectors $v_1, v_2, ... v_n \in R^n$, the span is equal to the column space of some matrix $A$. For this matrix $A$, there exists a vector $c$ such that $A^T Ac = A^T x$ 