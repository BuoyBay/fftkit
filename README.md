# Radix-2 FFT

Source-only radix-2 complex FFTs and symmetric spectral windows, inspired by
[Roger Meier's FFT Suite](https://opensource.the-meiers.org/). `Import fftkit`.
No Complex Utilities, native FFT library or plotting dependency is required.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add fftkit --git https://github.com/BuoyBay/fftkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer fftkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```


## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
