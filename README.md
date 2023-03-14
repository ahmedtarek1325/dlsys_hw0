# DL systems HW0
This is assignment is a part of [DL-systems course presented by CMU](https://dlsyscourse.org/). 



## What you will find in this repo
This hw is just a warm up for the course. Navigating this repo, you will find implementation for the following: 
- How to read [mnist data](http://yann.lecun.com/exdb/mnist/) 
- Softmax Loss
- Softmax regression on one epoch
- a Two layer Neural Net on one epoch
- softmax regression implemented in CPP 




## Tests
To run tests you can use the following commands in the repo directory: 
ps if you are running in jupyter add `!`  before the following commands
- `python3 -m pytest -k "softmax_loss"`
- `python3 -m pytest -k "softmax_regression_epoch and not cpp"`
- `python3 -m pytest -k "nn_epoch"`
-   `make`

    `python3 -m pytest -k "softmax_regression_epoch_cpp"`


## my AHA moments!!
 1. **Logical Mistake while implementing the softmx loss:** 
    * SOFTMAX eqution is $\ell_{\mathrm{softmax}}(z, y) = \log\sum_{i=1}^k \exp z_i - z_y.$

    at first I did it as if it was 
    
    $\ell_{\mathrm{softmax}}(z, y) = \log(\sum_{i=1}^k \exp (z_i - z_y))$

    and it **worked out** BUT WHY!!
    
    to answer this let's take it on multiple steps
    
    1. zy did enter the log as $\log(\exp(zy))$ which is equal to zy
    2. $\log\sum_{i=1}^k\exp(zi)) - \log(\exp(zy)) = \log(\frac{\sum_{i=1}^k\exp(zi)}{\exp(zy)})$
    3. $\log(\frac{\sum_{i=1}^k\exp(zi)}{\exp(zy)})$ = $\log(\sum_{i=1}^k\exp(zi-zy))$ 

    so this wrong formultion for softmaax still gave us right answer!. But we can see that it's computionally is very expensive as it calculates $z_i-z_y$ many many times!!. 

2. **why we do take log in softmax instead of softmax?**
    
    the softmax in literature is often written as $\frac{\exp(z_y)}{\sum_{i=1}^k \exp(z_i)}$, 

    But whenever we do it as a code we ususaly take the -log to reduce it to look like: 

    $\ell_{\mathrm{softmax}}(z, y) = \log\sum_{i=1}^k \exp z_i - z_y.$

    **The answer:** 

    This term $\sum_{i=1}^k \exp(z_i)$ is very big that if we put it in the denimerator we may encounter an underflow.
    **For simplicitly** Think of dividing 
    $\frac{1}{10000}\approx  0$

## Want to see more of the assignments ? 
### Click here to see the rest of the assignments and my take outts
1. [HW1](https://github.com/ahmedtarek1325/dlsys_hw1)
2. [HW2](https://github.com/ahmedtarek1325/dlsys_hw2)
3. [HW3](https://github.com/ahmedtarek1325/dlsys_hw3)
4. [HW4](https://github.com/ahmedtarek1325/dlsys_hw4)

## Refrences: 
1. [I used this help from stack overflow community to read the idx3 ubyte files](https://stackoverflow.com/questions/40427435/extract-images-from-idx3-ubyte-file-or-gzip-via-python)  
2. [Lectures from 1-3 to understand the theory](https://dlsyscourse.org/lectures/)
