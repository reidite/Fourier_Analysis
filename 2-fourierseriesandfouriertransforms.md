# Fourier series and Fourier transforms

Naturally, the discrete and continuous formulations should match the limit of data with infinitely fine resolution. The Fourier series and transform are intimately related to the geometry of infinite-dimensional function spaces, or Hilbert spaces, which generalize the notion of vector space to include functions with infinitely many degrees of freedom.

## Inner products of functions and vectors

## Fourier series

A fundamental result in Fourier analysis is that if $$f(x)$$is periodic and piecewise smooth, then it can be written in terms of a Fourier series, which is an infinite sum of cosines and sines of increasing frequency. In particular, if$$f(x)$$ is $$2\pi$$- periodic, it may be written as:

The coefficients ![formula](https://render.githubusercontent.com/render/math?math=a_k) and ![formula](https://render.githubusercontent.com/render/math?math=b_k) are given by

 ![](https://latex.codecogs.com/gif.latex?a_k&space;=&space;\frac{1}{\pi}&space;\int_{-\pi}^{\pi}&space;f%28x%29cos%28kx%29dx)  
 ![](https://latex.codecogs.com/gif.latex?b_k%20%3D%20%5Cfrac%7B1%7D%7B%5Cpi%7D%20%5Cint_%7B-%5Cpi%7D%5E%7B%5Cpi%7D%20f%28x%29sin%28kx%29dx) 

which may be viewed as the coordinates obtained by projecting the function onto the orthogonal cosine and sine basis ![](https://latex.codecogs.com/gif.latex?%5Cleft%20%5C%7B%20cos%28kx%29%2C%20sin%28kx%29%20%5Cright%20%5C%7D_%7Bk%3D0%7D%5E%7B%5Cinfty%7D). In other words, the integrals may be re-written in terms of the inner product as:

 ![](https://latex.codecogs.com/gif.latex?a_k%3D%5Cfrac%7B1%7D%7B%5Cleft%20%5C%7C%20cos%28kx%29%20%5Cright%20%5C%7C%5E2%7D%5Cleft%20%5Clangle%20f%28x%29%2C%20cos%28kx%29%20%5Cright%20%5Crangle)  
 ![](https://latex.codecogs.com/gif.latex?b_k%3D%5Cfrac%7B1%7D%7B%5Cleft%20%5C%7C%20sin%28kx%29%20%5Cright%20%5C%7C%5E2%7D%5Cleft%20%5Clangle%20f%28x%29%2C%20sin%28kx%29%20%5Cright%20%5Crangle)

where ![](https://latex.codecogs.com/gif.latex?%5Cleft%20%5C%7C%20cos%28kx%29%20%5Cright%20%5C%7C%5E2%3D%5Cleft%20%5C%7C%20sin%28kx%29%20%5Cright%20%5C%7C%5E2%3D%5Cpi). This factor of ![](https://latex.codecogs.com/gif.latex?%5Cfrac%7B1%7D%7B%5Cpi%7D) is easy to verify by numerically integrating $$cos(x)^2$$and $$sin(x)^2$$from $$-\pi$$to $$\pi$$.

The Fourier series for an$$L$$ - periodic function on $$[ 0, L)$$is similarly given by: $$f(x)=\frac{a_0}{2}+\sum_{k=1}^{\infty}{(a_kcos(\frac{2\pi kx}{L}+b_ksin(\frac{2\pi kx}{L})))}$$

with coefficients $$a_k$$and $$b_k$$ given by

$$a_k=\frac{2}{L} \int_{0}^{L}f(x)cos(\frac{2\pi kx}{L})dx$$ $$b_k=\frac{2}{L} \int_{0}^{L}f(x)sin(\frac{2\pi kx}{L})dx$$

Because we are expanding functions in terms of sine and cosine functions, it is also natural to use Euler's formular $$e^{ikx}=cos(kx)+i sin(kx)$$ to write a Fourier series in complex form with complex coefficients $$c_k=\alpha_k+i\beta_k$$ :

$$f(x)=\sum_{k=-\infty}^{\infty}c_ke^{ikx}=\sum_{k=-\infty}^{\infty}(\alpha_k+i\beta_k)(cos(kx)+isin(kx))$$ $$=(\alpha_0+i\beta_0)+\sum_{k=1}^{\infty}{[(\alpha_{-k}+\alpha_{k})\cos(kx)+(\beta_{-k}-\beta_{k})\sin(kx)]}$$ $$+ i\sum_{k=1}^{\infty}{[(\beta_{-k}+\beta_{k})\cos(kx)-(\alpha_{-k}-\alpha_{k})\sin(kx)]}$$

If $$f(x)$$is real-valued, then $$\alpha_{-k} = \alpha_{k}$$ and $$\beta_{-k} = -\beta_{k}$$, so that $$c{-k}=\bar{c}_k$$_._ Thus, the function __$$\psi_k=e^{ikx}$$ __for  __$$k \in \mathbb{Z}$$ __provide a basis for periodic, complex-valued functions on an interval $$[0,2\pi)$$_. I_t is simple to see that these functions are orthogonal:

 __$$\left\langle \psi_j, \psi_k \right\rangle = \int{-\pi}^{\pi}e^{ijx}e^{-ikx}dx=\int{-\pi}^{\pi}e^{i(j-k)x}dx=[\frac{e^{i(j-k)x}}{i(j-k)}]{-\pi}^{\pi}$$\_\_

## Fourier transform

