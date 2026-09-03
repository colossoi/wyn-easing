# wyn/easing

Composable, GPU-friendly easing curves and interpolation primitives for Wyn.

The API follows the same split used by established JavaScript animation
libraries: easing transforms progress, while interpolation mixes values.

- `cubic_in_out(progress)` and the other easing functions transform normalized
  progress.
- `lerp(start, end, amount)` interpolates or extrapolates directly.
- `interpolate(easing, start, end, progress)` composes the two.

That separation replaces the ambiguous `smooth` and `smoother` helpers from
v0.1.0. Curve names now describe both the polynomial family and direction.

## Install

```toml
[dependencies]
easing = { package = "wyn/easing", version = "v0.2.0", github = "github.com/YOUR_ACCOUNT/wyn-easing" }
```

Bind the dependency's library root to a module:

```wyn
module Easing = import "pkg:easing"

def fade_in(elapsed: f32) f32 =
  Easing.interpolate(Easing.quint_in_out,
                     0.0f32, 1.0f32, elapsed)
```

For a curve value without interpolation:

```wyn
def opacity(progress: f32) f32 = Easing.cubic_in_out(progress)
```

## API

### Primitives

| Function | Behavior |
| --- | --- |
| `clamp01(value)` | Clamps to the closed interval `[0, 1]` |
| `lerp(start, end, amount)` | Linear interpolation; extrapolates outside `[0, 1]` |
| `interpolate(easing, start, end, progress)` | Applies easing, then interpolates |

### Curves

All built-in curves clamp their input to `[0, 1]` and return exact endpoint
values. A custom curve passed to `interpolate` controls its own domain and may
overshoot intentionally.

| Family | Accelerate | Decelerate | Symmetric |
| --- | --- | --- | --- |
| Linear | — | — | `linear` |
| Quadratic | `quad_in` | `quad_out` | `quad_in_out` |
| Cubic | `cubic_in` | `cubic_out` | `cubic_in_out` |
| Quartic | `quart_in` | `quart_out` | `quart_in_out` |
| Quintic | `quint_in` | `quint_out` | `quint_in_out` |
| Sine | `sine_in` | `sine_out` | `sine_in_out` |
| Exponential | `expo_in` | `expo_out` | `expo_in_out` |
| Circular | `circ_in` | `circ_out` | `circ_in_out` |

The package also provides derivative-continuous polynomial fades with explicit
names:

- `smoothstep_cubic` — cubic Hermite, C1 continuous.
- `smoothstep_quintic` — Perlin's quintic fade, C2 continuous.

## Migration from v0.1.0

v0.2.0 intentionally removes the ambiguous convenience names:

| v0.1.0 | v0.2.0 |
| --- | --- |
| `linear(a, b, t)` | `lerp(a, b, t)` |
| `smoothstep(t)` | `smoothstep_cubic(t)` |
| `smootherstep(t)` | `smoothstep_quintic(t)` |
| `smooth(a, b, t)` | `interpolate(smoothstep_cubic, a, b, t)` |
| `smoother(a, b, t)` | `interpolate(smoothstep_quintic, a, b, t)` |

## Publish from GitHub

Commit `wyn.toml`, `src/`, `README.md`, and `CHANGELOG.md`, then create the tag
named by the manifest version:

```sh
git add wyn.toml src/lib.wyn README.md CHANGELOG.md
git commit -m "Release wyn/easing v0.2.0"
git tag v0.2.0
```

Wyn downloads the source archive for the declared tag when the package is first
built or checked.

## Development

Check both the implementation and the consumer-facing API before release:

```sh
wyn check .
wyn check test/api
```
