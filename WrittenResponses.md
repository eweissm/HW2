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
 
 $$ with\  \partial x_i = x_i - 1$$

If we solve for f(X) -f(X_0) and simplify some terms, we get

$$ f(X) -f(X_0) = 4\partial x_1^2-8\partial x_1 \partial x_2+3 \partial x_2^2= (2 \partial x_1 - 3 \partial x_2)(2 \partial x_1 - 1 \partial x_2)$$

Therefore the slope is downward for any set of X values which satisfies the question 

$$(2 (x_1 - 1) - 3 (x_2 - 1))(2 (x_1 - 1) - 1 (x_2 - 1)) < 0 $$

# Question 2

## Part A
This problem can be rewritten as 

$$ min \ \sqrt{ (x_1 +1)^2 + (x_2)^2 + (x_3 -1)^2} $$

$$S.T.\ x_1+2x_2+3x_3 = 1$$

We can simplify the objective by removing the square root and we can remove the constraint by substituting the contraint into the objective as such:

$$ min \  (2-2x_2-3x_3)^2 + (x_2)^2 + (x_3-1)^2 $$

We can prove this is a convex objective by finding the eigen values:

$$ g(X) = \begin{pmatrix}\ 10x_2+12x_3-8\\ 
12x_2+20x_3-14\end{pmatrix}$$

$$H = \begin{pmatrix}10&12\\
12&20\end{pmatrix}$$

 $$ \left| \begin{pmatrix}10-\lambda&12\\
12&20-\lambda\end{pmatrix} \right| = 0 $$

$$ λ=2,28 $$ 

Therefore the hessian is P.D., meaning the objective is convex

## Part B
We can easily find the exact values using analytical methods and this give us that the solution is

$$X = \begin{pmatrix} -\frac{15}{14}\\
-\frac{1}{7}\\
\frac{11}{14}\end{pmatrix}$$
We will use this to find our convergence.

note: I coded this in matlab as I am more comfortable using Matlab and we did not need to use the python optimizations. 

### Gradient Decent

```
initguessX2= 1;
initguessX3= 1;

initGuess= [1-2*initguessX2-3*initguessX3, initguessX2, initguessX3];

X=initGuess;

n = 1000;
distances=[];
X1 = [];
X2 = [];
X3 = [];
gTemp = [];
H = [ 10 12,
    12 20];
stop = [0,
    0];

for i = 1:n
    
    X1(end+1)= X(1);
    X2(end+1)= X(2);
    X3(end+1)= X(3);
    
    gTemp = g(X(2), X(3));
  if(gTemp == stop)
        break;
    end
   alpha=  (gTemp.'*gTemp)/(gTemp.'*H*gTemp);
    
    X(2)= X(2) - alpha*gTemp(1);
    X(3)= X(3) - alpha*gTemp(2);
     
    distances(end+1) = d( X(2), X(3));
    X(1)= 1-2*X(2)-3*X(3);
    
end
X

dExact= d(-1/7, 11/14);
k=1: length(distances);
conv = abs(dExact- distances );
plot(k,  conv)
set(gca, 'YScale', 'log');


[Y,Z] = meshgrid(-3:1:3,-3:1:3);
A=-2*Y-3*Z+1;


figure;
hold on;
plot3(-1,0, 1,'.r', 'MarkerSize',15 )
plot3(initGuess(1),initGuess(2),initGuess(3),'.g', 'MarkerSize',25 )
plot3(X1, X2, X3,'.b', 'MarkerSize',10 )

surf(A,Y,Z,'FaceAlpha',0.5)


function dist = d(x2,x3)
dist = (2-2*x2-3*x3)^2 +(x2)^2+(x3-1)^2; 
end

function grad = g(x2,x3)
grad = [10*x2+12*x3-8,
   12*x2+20*x3-14 ]; 
end
```
For initial guess $x_2 = 1,\ x_3=1$ the output closest point is 

$$X = \begin{pmatrix} -1.071428571428571\\
-0.142857142857143\\
0.785714285714286\end{pmatrix}$$

And the convergence is 

![untitled2](https://user-images.githubusercontent.com/73143081/190884025-e5e0153d-ccdd-486f-a941-7386afa218c8.jpg)

note: the y-axis is the $log(|f(k) - f_{exact}|)$ and the x axis is k

For initial guess $x_2 = 0,\ x_3=0$ the output closest point is 

$$X = \begin{pmatrix} -1.071428571428572\\
-0.142857142857143\\
0.785714285714286\end{pmatrix}$$

And the convergence is 

![untitled3](https://user-images.githubusercontent.com/73143081/190884104-755b4e65-d9da-4c25-adb7-631682cdf3d8.jpg)

note: the y-axis is the $log(|f(k) - f_{exact}|)$ and the x axis is k

For initial guess $x_2 = 50,\ x_3=50$ the output closest point is 

$$X = \begin{pmatrix} -1.071428571428572\\
-0.142857142857143\\
0.785714285714286\end{pmatrix}$$

And the convergence is 

![untitled4](https://user-images.githubusercontent.com/73143081/190884159-fdafa545-5122-4119-98eb-b437a8e76fb6.jpg)

note: the y-axis is the $log(|f(k) - f_{exact}|)$ and the x axis is k

### Newtons Method
```
initguessX2= 13;
initguessX3=10;

initGuess= [1-2*initguessX2-3*initguessX3, initguessX2, initguessX3];

X=initGuess;

n = 100;
distances=[d(initGuess(2),initGuess(3))];
X1 = [];
X2 = [];
X3 = [];
gTemp = [];
H = [ 10 12,
    12 20];
stop = [0,
    0];

for i = 1:n
    
    X1(end+1)= X(1);
    X2(end+1)= X(2);
    X3(end+1)= X(3);
    
    gTemp = g(X(2), X(3));

    dx= -inv(H)*gTemp;
    
    if(dx == stop)
        break;
    end
   alpha=  (gTemp.'*gTemp)/(gTemp.'*H*gTemp);
    X(2)= X(2) +dx(1);
    X(3)= X(3) +dx(2);
     
    distances(end+1) = d( X(2), X(3));
    X(1)= 1-2*X(2)-3*X(3);
    
end
X

dExact= d(-1/7, 11/14);
k=1: length(distances);
conv = abs(dExact- distances );
plot(k,  conv)
set(gca, 'YScale', 'log');


[Y,Z] = meshgrid(-3:1:3,-3:1:3);
A=-2*Y-3*Z+1;


figure;
hold on;
plot3(-1,0, 1,'.r', 'MarkerSize',15 )
plot3(initGuess(1),initGuess(2),initGuess(3),'.g', 'MarkerSize',25 )
plot3(X1, X2, X3,'.b', 'MarkerSize',10 )

surf(A,Y,Z,'FaceAlpha',0.5)


function dist = d(x2,x3)
dist = (2-2*x2-3*x3)^2 +(x2)^2+(x3-1)^2; 
end

function grad = g(x2,x3)
grad = [10*x2+12*x3-8,
   12*x2+20*x3-14 ]; 
end
```
For initial guess $x_2 = 13,\ x_3=10$ the output closest point is 

$$X = \begin{pmatrix} -1.071428571428572\\
-0.142857142857143\\
0.785714285714286\end{pmatrix}$$

And the convergence is 

![untitled5](https://user-images.githubusercontent.com/73143081/190884434-0e30a3f4-9ae6-4e56-9933-4aaf355e23dc.png)

note: the y-axis is the $log(|f(k) - f_{exact}|)$ and the x axis is k


For initial guess $x_2 = 0,\ x_3=0$ the output closest point is 

$$X = \begin{pmatrix} -1.071428571428572\\
-0.142857142857143\\
0.785714285714286\end{pmatrix}$$

And the convergence is 

![untitled6](https://user-images.githubusercontent.com/73143081/190884476-e2466f43-3916-49b1-a69b-8a0dc9a60608.jpg)

note: the y-axis is the $log(|f(k) - f_{exact}|)$ and the x axis is k


Clearly, the newtons method converges significantly faster. With lucky initial conditions, it could converge in as little as 2 interations as opposed to gradient decent needed nearly 30 iterations. 
# Question 3

A hyperplane can be written as 

$$ a^T x = c$$

which we can find the gradient and then the hessian for:

$$ \bigtriangledown_x  a^T x \=   a^T$$

$$H(a^T) = 0 \ (zero\ matrix) $$

Because H = 0, the eigen values would all equal 0, and therefore the hessian is P.S.D, meaning the plane must be convex. This can also be determined logically by thinking of a plane in any dimension. They will all be linear and therefore must be convex.

# Question 4

## Part A
For a problem to be convex the objective and the domain must be convex.
The domain of the fucntion is 

$$ 0 \leq p_i \leq p_{max} $$

to prove this we could analyze a system where i = 1, 2. Therefore we have 2 lights. 

We can graph the domain of p values for each light as below

![image](IMG_1452.jpg)

clearly this is a convex domain. As the number of lights increases this domain enters more dimensions, but the same principles apply and the domain remains convex.

Now we need to prove the objective is convex. The objextive is:

$$ {max}_k \ (h(a_k^T p, I_t)) $$

The max of a set of functions is convex so we need only prove that h is convex WRT p for any given k

$$ h(I, I_t) = 
    \begin{array}{lr}
        I_t/I, & \text{if } I \leq I_t\\
         I/I_t, & \text{if } I_t \leq I
    \end{array}
 $$ 

$$G(h) = \frac{\partial h}{\partial p} = \frac{dh}{dI} * \frac{\partial a^T P}{\partial p} = h'*a^T$$

$$H(h) =  \frac{\partial^2 h}{\partial p^2} = \frac{dh'}{dI} * \frac{\partial a^T P}{\partial p}*a^T = h''aa^T$$

we know $aa^T$ is a mxm matrix which must be P.S.D. so it must be convex. So now we need to  show that h is convex. This can be shown visually 

![IMG_1453](https://user-images.githubusercontent.com/73143081/190832484-92f70ae8-374a-478d-8fe1-6837edd4b44d.jpg)

Therefore, because H WRT I is convex, h'' must be a number greater than 0. Therefore the objective is convex WRT P.
Now both the objective and the domain are convex, so the problem is convex. 

## Part B

## Part C
In order to answer this question we must first show whether the hessian of h is P.D or P.S.D because as we showed in class a strictly convex problem will have a hessian that is P.D and will therefore have a unique solution. We know that P is a vector with n values and $a_k$ will be a vector with m values. As we showed in part A, the hessian of h is $h''aa^T$ which would be a mxm matrix scaled by h''. 

$$\text{If } w \neq 0 \text{ and } w \in \mathbb{R}^n $$

Then if

$$w^ta=y \ and\ a^tw=y$$

$$h''y^2 \geq 0 $$

In order for $y^2$ to be equal to zero the dimensions of w would need to be greater than the dimensions of a, or in other words n>m. Therefore, if n>m we could have a P.S.D. hessian for h and we could have infinite solutions. Likewise, if m = n, we would have a P.D. hessian and therefore we could have only 1 unique solution. 
So to answer the question, if we has 10 mirrors, we would have a unique solution, if we have less then 10 mirrors we would potentially have infinite solutions and if we had more than 10 mirrors we could have no solution.  

# Question 5
To start, the max of any set of convex functions is convex so we only need to prove that xy-c(x) is convex for any given A. Next we will find the hessian of the function WRT y:

$$g = \frac{dc^\star}{dy}= x$$

$$h = \frac{d^2c^\star}{dy^2}= 0$$

Hessian is zero, so the eigen value is zero, so the function is P.S.D. so therefore the function is convex
