<h1 align="center">
<p> Fourier and Wavelet :memo:</p>
<p align="center">
<img alt="ubuntu" src="https://img.shields.io/badge/ubuntu-%3E%3D18.04-blueviolet?style=for-the-badge&logo=ubuntu">
<img alt="python" src="https://img.shields.io/badge/python-%3E%3D3.6-blue?style=for-the-badge&logo=python">
<img alt="numpy" src="https://img.shields.io/badge/numpy-%3E%3D1.19-skyblue?style=for-the-badge&logo=numpy">
</p>
</h1>
<h1 align="left">
<p> Table of Contents </p>
</h1>

- [Introduction](#introduction)
- [Fourier series and Fourier transforms](#fourier-series-and-fourier-transforms)
  - [Inner products of functions and vectors](#inner-products-of-functions-and-vectors)
  - [Fourier series](#fourier-series)
  - [Fourier transform](#fourier-transform)
- [Discrete Fourier transform (DFT) and fast Fourier Transform (FFT)](#discrete-fourier-transform-dft-and-fast-fourier-transform-fft)
- [Transforming partial differential equations](#transforming-partial-differential-equations)
- [Gabor transform and the spectrogram](#gabor-transform-and-the-spectrogram)
- [Wavelet and multi-resolution analysis](#wavelet-and-multi-resolution-analysis)
- [2D transforms and image processing](#2d-transforms-and-image-processing)
- [References](#references)

## Introduction
The most foundational and ubiquitous coordinate transformation was introduced by J,-B. Joseph Fourier in the early 1800s in investigate the theory of heat [[1](#jean-baptiste-joseph-fourier-the-analytical-theory-of-heat-the-university-press-1878)]. Fourier introduced the concept that sine and cosine functions of increasing frequency provide an orthogonal basis for the space of solution functions. Indeed, the Fourier transform basis of sines and cosines serve as eigenfunctions of the heat equation, with the specific frequncies serving as the eigenvalues, determined by the geometry, and amplitudes determined by the boundary conditions.

Fourier's seminal work provided the mathematical foundation for Hilbert spaces, operator theory, approximation theory, and the subsequent revolution in analytical and computational mathematics. Fast forward two hundred years, and the fast Fourier transform has become the cornerstone of computational  mathematics, enabling real-time image and audio compression, global communication networks, mordern devices and hardware, numerical physics and enineering at scale, and advanced data analysis. Simply put, the fast Fourier transform has had a more significant and profound role in shaping the modern world than any other algorithm to date.

With increasingly complex problems, data sets, and computational geometries, simple Fourier sine and cosine bases have given way to tailored bases, such as the data-driven SVD. In fact, the SVD basis can be used as a direct analogue of the Fourier basis for solving PDEs with complex geometries. In addition, related functions, called wavelets, have been developed for advanced signal processing and compression efforts.

## Fourier series and Fourier transforms
Naturally, the discrete and continous formulations should match in the limit of data with infinitely fine resolution. The Fourier series and transform are intimately related to the geometry of infinite-dimensional function spaces, or Hillbert spaces, which generalize te notion of vector space to include functions with infinitely many degrees of freedom.
### Inner products of functions and vectors

### Fourier series
A fundamental result in Fourier analysis is that if $f(x)$ is periodic and piecewise smooth, then it can be written in term of a Fourier series, which is an infinite sum of cosines and sines of increasing frequency. In particular, if $f(x)$ is $2\pi$-periodic, it may be written as:

$$f(x)=\frac{a_0}{2} + \sum_{k-1}^{\infin}(a_kcos(kx) + b_ksin(kx))$$

The coefficients $a_k$ and $b_k$ are given by
$$a_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x)cos(kx)dx$$
$$b_k = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x)sin(kx)dx$$
which may be viewed as the coordinates obtained by projecting the function onto the orthogonal cosine and sine basis $\left \{ cos(kx), sin(kx) \right \}_{k=0}^{\infin}$. In other words, the integrals in may be re-written in terms of the inner product as:

$$a_k=\frac{1}{\left \| cos(kx) \right \|^2}\left \langle f(x), cos(kx)  \right \rangle$$
$$b_k=\frac{1}{\left \| sin(kx) \right \|^2}\left \langle f(x), sin(kx)  \right \rangle$$

where $\left \| cos(kx) \right \|^2=\left \| sin(kx) \right \|^2=\pi$. This factor of $\frac{1}{\pi}$ is easy to verify by numerically integrating $cos(x)^2$ and $sin(x)^2$ from $-\pi$ to $\pi$.

The Fourier series for an $L$-periodic function on $[ 0, L)$ is similarly given by:
$$f(x)=\frac{a_0}{2}+\sum_{k=1}^{\infin}{(a_kcos(\frac{2\pi kx}{L}+b_ksin(\frac{2\pi kx}{L})))}$$

with coefficients $a_k$ abd $b_k$ given by

$$a_k=\frac{2}{L} \int_{0}^{L}f(x)cos(\frac{2\pi kx}{L})dx$$
$$b_k=\frac{2}{L} \int_{0}^{L}f(x)sin(\frac{2\pi kx}{L})dx$$

Because we are expanding functions in terms of sine and cosine functions, it is also natural to use Euler's formular $e^{ikx}=cos(kx)+i sin(kx)$ to write a Fourier series in complex form with complex coefficients $c_k=\alpha_k+i\beta_k:$

$$f(x)=\sum_{k=-\infin}^{\infin}c_ke^{ikx}=\sum_{k=-\infin}^{\infin}(\alpha_k+i\beta_k)(cos(kx)+isin(kx))$$
$$=(\alpha_0+i\beta_0)+\sum_{k=1}^{\infin}{[(\alpha_{-k}+\alpha_{k})\cos(kx)+(\beta_{-k}-\beta_{k})\sin(kx)]}$$
$$+ i\sum_{k=1}^{\infin}{[(\beta_{-k}+\beta_{k})\cos(kx)-(\alpha_{-k}-\alpha_{k})\sin(kx)]}$$

If $f(x)$ is real-valued, then $\alpha_{-k} = \alpha_{k}$ and $\beta_{-k} = -\beta_{k}$, so that $c_{-k}=\bar{c}_k$. Thus, the function $\psi_k=e^{ikx}$ for $k \in \mathbb{Z}$ provide a basis for periodic, complex-valued functons on an interval $[0,2\pi)$. It is simple to see that these functions are orthogonal:
$$\left\langle \psi_j, \psi_k \right\rangle = \int_{-\pi}^{\pi}e^{ijx}e^{-ikx}dx=\int_{-\pi}^{\pi}e^{i(j-k)x}dx=[\frac{e^{i(j-k)x}}{i(j-k)}]_{-\pi}^{\pi}$$

### Fourier transform


## Discrete Fourier transform (DFT) and fast Fourier Transform (FFT)

## Transforming partial differential equations

## Gabor transform and the spectrogram

## Wavelet and multi-resolution analysis

## 2D transforms and image processing

## References

- #### [Jean Baptiste Joseph Fourier. The analytical theory of heat. The University Press, 1878](https://www.cambridge.org/core/books/analytical-theory-of-heat/F6D4802336FABD1116DDA4AA3FE6EFAA).


<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.3/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>