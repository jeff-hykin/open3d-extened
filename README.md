# open3d-unofficial-arm

Universal Open3D package that works on **all platforms** including ARM64.

## Installation

```bash
pip install open3d-unofficial-arm
```

Works everywhere:
- **ARM64 Linux**: Installs pre-built ARM wheels (Python 3.10, 3.11, 3.12, 3.13)
- **Other platforms** (x86_64, macOS, Windows): Automatically installs official `open3d`

## Usage

```python
import open3d as o3d  # Same on all platforms!

# Use exactly like normal
pcd = o3d.geometry.PointCloud()
print(o3d.__version__)
```

**Zero code changes.** Works identically to the official package.

## How It Works

This package uses **conditional dependencies** (PEP 508 environment markers):

```toml
dependencies = [
    "open3d>=0.18.0; platform_machine != 'aarch64'"
]
```

### On ARM64:
- Installs ARM-specific wheels bundled with this package
- Provides `open3d` package directly

### On other platforms:
- pip installs official `open3d` as a dependency
- You get the official package with full support

This is the **standard, non-hacky way** to provide platform-specific packages in Python!

## Why This Package?

- Official Open3D doesn't publish ARM64 wheels yet
- This fills the gap for ARM users
- Also works as a drop-in on other platforms for convenience
- Single `pip install` command works everywhere

## Platform Support

| Platform | Source | Status |
|----------|--------|--------|
| ARM64 Linux (aarch64) | This package | ✅ 0.19.0 |
| x86_64 Linux | Official open3d | ✅ Latest |
| macOS (Intel/Apple Silicon) | Official open3d | ✅ Latest |
| Windows | Official open3d | ✅ Latest |

## Relationship to Official Open3D

- **NOT** affiliated with or endorsed by the Open3D project
- Unofficial community build for ARM platforms
- Use official `open3d` when ARM support is available
- Official project: https://github.com/isl-org/Open3D

## For Maintainers

### Building ARM Wheels

1. Get ARM wheels named `open3d-*.whl`
2. Run rename script:
   ```bash
   python rename_wheels.py
   ```
3. Upload to PyPI:
   ```bash
   ./run/publish
   ```

The script:
- Keeps package name as `open3d` (preserves imports)
- Changes distribution name to `open3d-unofficial-arm`
- Updates version from `pyproject.toml`

## License

MIT License - See LICENSE file.

Open3D code is subject to the MIT license. See https://github.com/isl-org/Open3D for details.

## Support

- **ARM wheel issues**: Open an issue in this repository
- **Open3D bugs/features**: Report to official Open3D project
- Works identically to official package on all platforms
