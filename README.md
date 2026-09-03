# wyn/easing

Small interpolation helpers for Wyn animation and procedural graphics.

The package exports:

- `clamp01(x)`
- `linear(a, b, t)`
- `smoothstep(t)` and `smooth(a, b, t)`
- `smootherstep(t)` and `smoother(a, b, t)`

## Publish from GitHub

Create a repository containing this directory's `wyn.toml`, `src/`, and
`README.md` at its root. Commit the files and create the tag named by the
manifest version:

```sh
git init
git add wyn.toml src/lib.wyn README.md
git commit -m "Publish wyn/easing v0.1.0"
git tag v0.1.0
```

After pushing the repository and tag, a consumer can declare it as follows,
replacing `YOUR_ACCOUNT` with the GitHub owner:

```toml
[dependencies]
easing = { package = "wyn/easing", version = "v0.1.0", github = "github.com/YOUR_ACCOUNT/wyn-easing" }
```

Bind the dependency's library root to a module in Wyn source:

```wyn
module Easing = import "pkg:easing"

def fade_in(elapsed: f32) f32 = Easing.smoother(0.0f32, 1.0f32, elapsed)
```

Wyn downloads GitHub's source archive for tag `v0.1.0` when the package is
first built or checked.
