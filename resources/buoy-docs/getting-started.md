---
title: "Fourier transforms getting started"
summary: "Use fftkit with a complete example and explicit numerical conventions."
category: "Guides"
order: 10
keywords: ["fftkit", "example", "import"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

## Prepare the package

Place the sealed `fftkit-0.1.0.buipkg` archive in your project's `packages/` directory. The example imports the package by its manifest name and uses explicit methods.

## First use

Choose a power-of-two sample count. Use `ForwardFFT` for real samples or `TransformFFT` for separate real and imaginary arrays. An inverse transform sets the third argument to true and divides by the transform length. Windowing and padding are explicit steps rather than hidden normalization.

```basic
Import fftkit

Sub Main()
    Dim samples As Array Of Double = [1.0, 0.0, 0.0, 0.0]
    Dim spectrum As FFTResult = ForwardFFT(samples)
    For Each value As Double In spectrum.Real
        Print value
    Next
    Dim restored As FFTResult = TransformFFT(spectrum.Real, spectrum.Imaginary, True)
    Print restored.Real(0)
End Sub
```

## Conventions

The forward convention is X[k] = sum(x[n] * exp(-2*pi*i*k*n/N)) and is unnormalized. The inverse uses the positive sign and divides by N. Real input returns all N complex bins, including the conjugate half. Windows are symmetric with denominator N-1; a singleton window is [1.0]. Hamming uses 0.54/0.46 coefficients. Window gain, amplitude scaling, sample rate, and frequency axes are never inferred. Zero padding interpolates spectral samples without increasing underlying spectral resolution. Iterative work is O(N log N) with O(N) additional storage; the allocation cap is not a latency guarantee.

## Handle invalid inputs

Transform sizes must be powers of two from 1 through 1,048,576, and the real and imaginary inputs must have equal lengths. Invalid sizes, mismatched lengths, and invalid padding throw `InvalidArgumentException`. Nonfinite sample values are not rejected; callers must supply finite inputs if they require finite results. Results remain mutable, not cached immutable spectra.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
