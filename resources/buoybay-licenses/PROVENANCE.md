# Source and parity

Source: [FFT Suite v1.0](https://opensource.the-meiers.org/FFT_Suite_v1.0.zip),
linked from [Roger Meier's public-domain projects](https://opensource.the-meiers.org/).
Archive SHA-256: `b06abe329243681425a42238efade438277cdf37f8bf07b9d94e221f3aba7031`.

The ZIP contains `FFT Demo.rbp` and `FFT_Suite.rbo`, plus Mac metadata. The binary
module's embedded source strings were inspected. Its internal license note says
FFT Suite is public domain and may be used for any purpose, without warranty.
This package is a fresh Buoy implementation of standard transform algorithms
and window formulas, rather than a syntax translation or binary import.

| Original | FFTKit |
| --- | --- |
| Recursive `FFT_int` radix-2 Cooley-Tukey | Iterative bit-reversal/in-place butterflies on fresh copies |
| `FFT` overloads for Double and Complex arrays | `ForwardFFT` and separate real/imaginary `TransformFFT` |
| Optional FFT zero-padding length | Explicit `ZeroPadFFT` followed by transform |
| Invalid sizes return empty arrays | Throw `InvalidArgumentException`, with an explicit upper bound |
| No public inverse transform found in inspected declaration inventory | Explicit inverse with 1/N normalization |
| Box, Hanning, Hamming, Blackman windows | Rectangular, Hann, Hamming, Blackman |
| Original Hamming coefficients 0.53836 / 0.46164 | Conventional 0.54 / 0.46, deliberate numeric difference |
| Bartlett-Hanning, Blackman-Harris, Tukey, Bartlett, Nuttall, Blackman-Nuttall, FlatTop, Gauss, Welch, Kaiser/Bessel helpers | Not implemented |
| ZeroPad Complex overload | Pad real and imaginary arrays separately |
| Complex Utilities and DataPlot Demo dependencies | Independent numerical package and console demo |

Symmetric windows use N-1 in the denominator; periodic windows are not supplied.
The package does not implement real-spectrum packing, arbitrary-length FFTs,
STFTs, PSD estimation, convolution, automatic resampling or threaded/GPU FFTs.
These remain separate extensions. There is no claim to match original project
UI, complete source API, numeric corner-case behavior or plotting assets.
