# How to do Linear Regression the Right Way

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
