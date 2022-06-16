1. Enabling Factoring of Each Term's Power
   -Instead of a forced 0 coefficient to begin with, the beginning value/result coefficient can begin with any degree
      -Allows variability for every term instead of creating each term linearly
   -Removed need for x_to_the_i (power) variable or a separate loop for it
      -Each term no longer has to be created from the ground-up
    
    void poly(long a[], long x, long degree, long *value)
    {
            
     long i;
     *value = a[degree];

     for ( i = degree - 1; i >= 0; i-- )
     {
              
       (*value) = a[i] + x * (*value);
              
     }
            
   }
   
Processor Clock Rate ~= 1.1984 GHz (extracted from file)
Poly pace 2.01 cycles per element
Poly still works


2. Loop Unroll & Iteration Reduction
   -Degrees first, squared and cubed are declared
      -Optimizes the time it takes to create these terms
   -New for-loop increments the creation of each term (using polynomial equation)
      -Needed to avoid stalling their individual creation
   -Another for-loop is used for constants and remaining terms
      -Allows for smooth and consistent iterations without any terms taking too long
    
    void poly(long a[], long x, long degree, long *value)
    {

      long i;
      long x_sqrd = x * x;
      long x_cubed = x_sqrd * x;
      *value = a[degree];

      for ( i = degree - 1; i >= 2; i-= 3 )
          (*value) = a[i - 2] + x * a[i - 1] + x_sqrd * a[i] + x_cubed * (*value);
  
      for (i = 0; i >= 0; i-- )
          (*value) = a[i] + x * (*value);
  
    }
    
Processor Clock Rate ~= 1.1973 GHz (extracted from file)
Poly pace 1.03 cycles per element
Poly still works
