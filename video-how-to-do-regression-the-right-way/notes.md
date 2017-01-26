# How to do Linear Regression the Right Way

``` python
def run():
    # step 1 - collect our data
    # in data.csv column 1 is hours studied
    # column 2 is the average grade
    points = genfromtxt('data.csv', delimiter=',')

    # step 2 - definte our hyperparameters
    # how fast should our model converge
    learning_rate = 0.0001
    # y=mx+b
    initial_b = 0
    initial_m = 0
    num_iterations = 1000

    #step 3 - train our model
    print 'starting gradient descent at b = {0}, m={1}, error = {2}'.format(initial_b,initial_m,compute_error_for_line_given_points(initial_b,initial_m,points))
    [b,m] = gradient_descent_runner(points, initial_b, initial_m, learning_rate, num_iterations)
    print 'after {0} iterations b = {1}, m={2}, error = {3}'.format(num_iterations,b,m,compute_error_for_line_given_points(b,m,points))

if __name__ == '__main__':
    run()

```
This function is where we will initialize our vars and then  to do the work and then they will report back here

`__name__` is where the meat of the code goes

`from numpy import *` when this syntax used to import model you no longer have
to write the name i.e `numpy.mean()` every time you use it

### Calculating Error
`def compute_error_for_line_given_points` this start by basically drawing a random line
through the data and then to Calculate the error just calculate the distance between
each point and the line.  Then you sum all those distances.  {{{{intsert distance formula here}}}}

The equation is basically the summing of the distances from the line squaring them because we want
the error to be positive and we care more about the magnitude.  The equation boils down to the
summation of the y position of the point and the line so `(y - (mx+b))^2` where mx+b is the line.

practical use of linear regression
very good for finding relationship between two variables

``` python
def compute_error_for_line_given_points(b,m,points):
    #initialize error at 0
    totalError = 0
    # for every point
    for i in range(0,len(points)):
        #get the x value
        x = points[i,0]
        # get the y value
        y = points[i,1]
        # get the difference and add it to the total
        totalError += (y-(m*x+b)) ** 2
    # get the average
    return totalError/float(len(points))
```

### Run Gradient Descent

``` python
def gradient_descent_runner(points, starting_b, starting_m, learning_rate, num_iterations):
    #starting b and m
    b = starting_b
    m = starting_m
    #gradient descent
    for i in range(num_iterations):
        # update b and m with the new more accurate b and m by performing gradient step
        b,m = step_gradient(b,m,array(points), learning_rate)
    return [b,m]
```

### Gradient Step Down

``` python
def step_gradient(b_current, m_current, points, learning_rate):
    # starting points for our gradients
    b_gradient = 0
    m_gradient = 0
    N = float(len(points))

    for i in range(0, len(points)):
        x = points[i, 0]
        y = points[i, 1]
        # direction with respect to b and m
        # computing partial derivatives of our error function
        # finding partial derivative gives you tangent line which gives you the direction
        b_gradient += -(2/N) * (y-((m_current * x) + b_current))
        m_gradient += -(2/N) * x * (y-((m_current * x)+ b_current))
    # update our b and m values using our partial derivatives
    new_b = b_current - (learning_rate * b_gradient)
    new_m = m_current - (learning_rate * m_gradient)
    return [new_b, new_m]
```
