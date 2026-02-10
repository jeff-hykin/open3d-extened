# Publishing to PyPI

This package uploads the ARM wheels directly to PyPI using the professional approach.

## What Gets Uploaded

Four separate wheel files:
- `open3d_unofficial_arm-0.19.0-cp310-cp310-manylinux_2_35_aarch64.whl`
- `open3d_unofficial_arm-0.19.0-cp311-cp311-manylinux_2_35_aarch64.whl`
- `open3d_unofficial_arm-0.19.0-cp312-cp312-manylinux_2_35_aarch64.whl`
- `open3d_unofficial_arm-0.19.0-cp313-cp313-manylinux_2_35_aarch64.whl`

Each wheel:
- Is ~46 MB (under PyPI's 100 MB limit per file)
- Contains the `open3d` package (so `import open3d` works)
- Has distribution name `open3d-unofficial-arm` (so it doesn't conflict with official package)

## Publishing

Simply run:

```bash
./run/publish
```

This will:
1. Run `rename_wheels.py` to create properly named wheels
2. Validate all wheels with `twine check`
3. Upload all 4 wheels to PyPI
4. Tag the git version

## User Experience

After publishing, users can:

```bash
# Install
pip install open3d-unofficial-arm

# Use (no code changes!)
import open3d as o3d
```

## How It Works (Professional Approach)

This is exactly how numpy, torch, tensorflow, etc. work:

1. Multiple wheels uploaded to PyPI (one per Python version/platform)
2. pip sees all available wheels
3. pip selects the wheel matching user's platform and Python version
4. pip downloads and installs only that wheel

No bundling, no runtime downloads, no hacks - just standard PyPI behavior!

## Version Numbering

Version is set in `pyproject.toml` - currently not used for wheel building, but kept for compatibility with the publish script versioning.

The actual version comes from the wheel filenames (0.19.0 for Open3D).
