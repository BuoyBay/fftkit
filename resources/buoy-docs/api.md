---
title: "Fourier transforms API"
summary: "Public fftkit symbols and numerical contracts."
category: "Reference"
order: 20
keywords: ["fftkit", "API", "reference"]
symbols: ["FFTResult", "FFTResult.Real", "FFTResult.Imaginary", "IsFFTSize", "TransformFFT", "ForwardFFT", "ZeroPadFFT", "RectangularWindow", "HannWindow", "HammingWindow", "BlackmanWindow", "ApplyFFTWindow"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

`Import fftkit` exposes these public types and operations.

| Symbol | Behavior |
| --- | --- |
| `FFTResult.Real / Imaginary As Array Of Double` | Fresh mutable transform output arrays; inputs remain unchanged even if they alias. |
| `IsFFTSize(length As Integer) As Boolean` | Check for a supported power of two in 1..1048576. |
| `TransformFFT(real, imaginary, inverse As Boolean = False) As FFTResult` | Transform equal-sized Double arrays; inverse changes sign and divides by N. |
| `ForwardFFT(samples As Array Of Double) As FFTResult` | Supply zero imaginary samples and return the complete complex spectrum. |
| `ZeroPadFFT(samples, length As Integer) As Array Of Double` | Return a fresh padded copy; length must fit input and lie in 1..1048576, but need not be a power of two. |
| `RectangularWindow(length) / HannWindow(length)` | Return symmetric Double weight arrays; lengths are 1..1048576. |
| `HammingWindow(length) / BlackmanWindow(length)` | Return conventional symmetric window weights with the same bounds. |
| `ApplyFFTWindow(samples, weights) As Array Of Double` | Return pairwise products without modifying inputs; equal empty arrays are allowed, unequal lengths or more than 1048576 elements reject. |

## Numerical behavior

The forward convention is X[k] = sum(x[n] * exp(-2*pi*i*k*n/N)) and is unnormalized. The inverse uses the positive sign and divides by N. Real input returns all N complex bins, including the conjugate half. Windows are symmetric with denominator N-1; a singleton window is [1.0]. Hamming uses 0.54/0.46 coefficients. Window gain, amplitude scaling, sample rate, and frequency axes are never inferred. Zero padding interpolates spectral samples without increasing underlying spectral resolution. Iterative work is O(N log N) with O(N) additional storage; the allocation cap is not a latency guarantee.

## Errors and ownership

Transform sizes must be powers of two from 1 through 1,048,576, and the real and imaginary inputs must have equal lengths. Invalid sizes, mismatched lengths, and invalid padding throw `InvalidArgumentException`. Nonfinite sample values are not rejected; callers must supply finite inputs if they require finite results. Results remain mutable, not cached immutable spectra.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)

[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
