---
title: "Fourier transforms"
summary: "Compute bounded radix-2 complex FFTs and symmetric spectral windows."
category: "Overview"
order: 0
keywords: ["fftkit", "mathematics", "numerical"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Fourier transforms

`fftkit` provides pure Buoy complex transforms, real-input convenience, zero padding, and symmetric window functions. It has no native FFT, complex-number, or plotting dependency. Inputs are copied, and returned real and imaginary arrays belong to the caller.

## Install

Copy `fftkit-0.1.0.buipkg` into the consuming application's `packages/` directory and use `Import fftkit`. The package is independently usable on macOS, Windows, and Linux. It requires no native bridge or drawing surface.

## Scope and provenance

This independent implementation is inspired by Roger Meier's FFT Suite. It deliberately uses iterative butterflies, explicit inverse normalization, and conventional Hamming coefficients. Arbitrary-length transforms, real-spectrum packing, periodic windows, STFT, PSD, convolution, GPU transforms, and many original window families are outside the package.

## Validation and limits

Transform sizes must be powers of two from 1 through 1,048,576, and the real and imaginary inputs must have equal lengths. Invalid sizes, mismatched lengths, and invalid padding throw `InvalidArgumentException`. Nonfinite sample values are not rejected; callers must supply finite inputs if they require finite results. Results remain mutable, not cached immutable spectra.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
