# Question 1
First we find the Gradient

$$ \bigtriangledown_x (2x_1^2 -4-x_1 x_2 +1.5x_2^2 +x_2) \=  \begin{pmatrix}4x_1-4x_2\\
 -4x_1+3x_2+1\end{pmatrix} $$
  
 Using this we can show that the stationary point is where the gradient is equal to zero by setting the gradient equal to zero and solving for x_1 and x_2. This gives us the stationary point as (1,1)
 Next we want to find the eigenvalues and to do this we use the hessian. 
 
 $$ H = \begin{pmatrix}4&-4\\
 -4&3\end{pmatrix}$$
 
 Then we find the eigen values 
 
 $$   \left|\begin{pmatrix}4 - \lambda &-4\\
 -4&3- \lambda\end{pmatrix} \right| = 0 $$
 
 Solving for the eigen values gives us
 
 $$ \lambda = \pm \frac{7+\sqrt{65}}{2} $$
 
 Because we have a positive and a negative eigen value at our stationary point, we know the point must be a saddle point.
 
 In order to find the directions of downward slope, we start with
 
 $$ f(x_1, x_2) = f(1,1) + g(1,1)(\partial X) + 1/2 \begin{pmatrix}\partial x_1&\partial x_2\end{pmatrix} \begin{pmatrix}4&-4\\
 -4&3\end{pmatrix}  \begin{pmatrix}\partial x_1 \\
 \partial x2\end{pmatrix}$$
