---
title: "fftkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["FFTResult"]
dependencies: []
symbols: ["FFTResult"]
related: ["api.md", "getting-started.md", "index.md"]
---

# fftkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## FFTResult

`Public Class FFTResult`

Separate real/imaginary transform outputs, owned by the caller.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Real` | `Array Of Double` | No | No | — | — |
| `Imaginary` | `Array Of Double` | No | No | — | — |

## FFTKit functions

### IsFFTSize

`Public Function IsFFTSize(length As Integer) As Boolean`

Return whether length is a supported radix-2 transform size.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `length` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### TransformFFT

`Public Function TransformFFT(real As Array Of Double, imaginary As Array Of Double, inverse As Boolean = False) As FFTResult`

Forward uses exp(-2*pi*i*k*n/N); inverse uses positive sign and divides by N. Inputs are copied and never modified, even if both arguments alias.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `real` | `Array Of Double` | `ByVal` | Required |
| `imaginary` | `Array Of Double` | `ByVal` | Required |
| `inverse` | `Boolean` | `ByVal` | `False` |

#### Returns

| Type |
| --- |
| `FFTResult` |

### ForwardFFT

`Public Function ForwardFFT(samples As Array Of Double) As FFTResult`

Real-input transform returns the complete N-bin complex spectrum.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `samples` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `FFTResult` |

### ZeroPadFFT

`Public Function ZeroPadFFT(samples As Array Of Double, length As Integer) As Array Of Double`

Fresh zero-padded copy; truncation is rejected. Does not imply a valid FFT size.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `samples` | `Array Of Double` | `ByVal` | Required |
| `length` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of Double` |

### RectangularWindow

`Public Function RectangularWindow(length As Integer) As Array Of Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `length` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of Double` |

### HannWindow

`Public Function HannWindow(length As Integer) As Array Of Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `length` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of Double` |

### HammingWindow

`Public Function HammingWindow(length As Integer) As Array Of Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `length` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of Double` |

### BlackmanWindow

`Public Function BlackmanWindow(length As Integer) As Array Of Double`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `length` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of Double` |

### ApplyFFTWindow

`Public Function ApplyFFTWindow(samples As Array Of Double, weights As Array Of Double) As Array Of Double`

Multiply samples by weights into a new array; neither input is modified.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `samples` | `Array Of Double` | `ByVal` | Required |
| `weights` | `Array Of Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Array Of Double` |
