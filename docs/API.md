# FFTKit 0.1.0

Pure Buoy radix-2 complex FFTs and symmetric spectral windows, inspired by
[Roger Meier's FFT Suite](https://opensource.the-meiers.org/). `Import fftkit`.
No Complex Utilities, native FFT library or plotting dependency is required.

## API

- `TransformFFT(real, imaginary, inverse = False) As FFTResult` accepts equally
  sized `Array Of Double` inputs. Returns fresh caller-owned `Real` and
  `Imaginary` arrays. Both inputs remain unchanged, including when they alias.
- `ForwardFFT(samples) As FFTResult` supplies zero imaginary samples and returns
  the complete N-bin complex spectrum, including the conjugate half.
- `IsFFTSize(length)` checks a power of two in `1..1048576`.
- `ZeroPadFFT(samples, length)` returns a fresh resizable padded copy. Target
  length must fit the input and lie in `1..1048576`; it need not be a power of
  two. Truncation rejects. Padding does not change spectral resolution.
- `RectangularWindow(length)`, `HannWindow(length)`, `HammingWindow(length)`,
  `BlackmanWindow(length)` return symmetric N-sample windows using denominator
  `N-1`. A one-sample window is `[1.0]`; empty windows reject. Window sizes
  need not be powers of two. Hamming uses conventional `0.54/0.46` coefficients.
- `ApplyFFTWindow(samples, weights)` returns pairwise products, rejecting unequal
  lengths or more than 1048576 elements. Empty matching inputs return empty.

Transform convention is `X[k] = sum(x[n] * exp(-2*pi*i*k*n/N))`. The forward
transform is unnormalized. Inverse uses the positive sign and divides by N.
Thus a unit sine at bin 3 of 32 samples gives `X[3] = -16i`, `X[29] = +16i`.
No amplitude/window-gain compensation, sample rate or frequency axis is inferred.

Length mismatches, invalid FFT sizes, invalid window sizes and invalid padding
throw `InvalidArgumentException`. Nonfinite values are not rejected: callers
must supply finite inputs and accept normal IEEE-754 propagation and overflow.
Numerical accuracy is floating-point, not exact; no large-length error guarantee
or performance benchmark is claimed. Maximum size is an allocation/work guard,
not a latency promise.

The iterative in-memory FFT uses O(N log N) work and O(N) additional storage.
It allocates fresh real/imaginary outputs, avoiding recursive subarray copies.
Returned arrays are mutable, not immutable cached spectra.

## Package scope

The transform and window functions are source-only and require no GUI or network
service. See the [source and parity notes](../PROVENANCE.md) for the scope of the
independent implementation and original API comparison.
