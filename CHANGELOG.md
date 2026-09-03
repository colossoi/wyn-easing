# Changelog

## v0.2.0

- Replaced `linear(a, b, t)` with the conventional `lerp` name.
- Replaced `smooth` and `smoother` with the composable `interpolate` function.
- Added flat, direction-explicit names modeled after established animation
  APIs: `quad_in`, `cubic_out`, `sine_in_out`, and their companion families.
- Gave the smoothstep variants explicit cubic/quintic names.
- Added quadratic, cubic, quartic, quintic, sine, exponential, and circular
  easing families.
- Defined consistent clamping and extrapolation behavior across the API.

## v0.1.0

- Initial release with linear interpolation and cubic/quintic smoothstep
  helpers.
