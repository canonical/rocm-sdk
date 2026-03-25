# ROCm SDK for Workshop

A development environment for AMD GPU compute projects. It provides the ROCm
runtime and development tools installed from the official AMD APT repository,
with GPU passthrough to the workshop.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: rocm-app
base: ubuntu@24.04
sdks:
  - name: rocm
    channel: 7.1/edge

actions:
  check: |
    rocminfo
  build: |
    hipcc main.cpp -o main
```

This demonstrates a basic ROCm workflow with GPU access for HIP compilation.

---

## Using the SDK

### Prerequisites, project layout

1. An AMD GPU with ROCm support must be available on the host.
2. Your HIP/ROCm project should be in your project directory:

   ```bash
   git clone <YOUR_REPO_URL>
   ```

3. On launch, the SDK installs the ROCm stack from the official AMD APT
   repository, configures `PATH`, library paths, and sets standard ROCm
   environment variables (`ROCM_PATH`, `HIP_PATH`, etc.).

### Build the project

Once the workshop is ready:

```bash
workshop shell
hipcc main.cpp -o main
```

Standard ROCm tools (`hipcc`, `rocminfo`, `rocm-smi`, `amdclang++`, etc.) are
available on PATH.

### Check GPU access

```bash
workshop shell
rocminfo
rocm-smi
```

### Environment variables

The SDK sets the following environment variables via `/etc/profile.d/rocm-sdk.sh`:

- `ROCM_PATH` — ROCm installation prefix (default `/opt/rocm`)
- `ROCM_HOME` — Same as `ROCM_PATH`
- `HIP_PATH` — HIP installation prefix
- `HSA_PATH` — HSA runtime prefix

### Customisation

The setup-base hook supports environment variable overrides:

- `ROCM_PACKAGES` — APT meta-package(s) to install (default: `rocm-dev`)
- `ROCM_INSTALL_PREFIX` — Installation prefix (default: `/opt/rocm`)

---

## Plugs (resources this SDK consumes)

### `gpu`

- Interface: `gpu`
- Purpose: Passes through the host GPU to the workshop for ROCm compute.

---

## Branch and release strategy

Each supported ROCm minor release series has its own branch:

| Branch | ROCm series | Renovate constraint |
|--------|-------------|---------------------|
| `6.3`  | 6.3.x       | `^6.3.`             |
| `7.0`  | 7.0.x       | `^7.0.`             |
| `7.1`  | 7.1.x       | `^7.1.`             |

Renovate monitors GitHub releases from
[ROCm/ROCm](https://github.com/ROCm/ROCm) and proposes patch-level updates
within each branch. The `VERSION` file is the single source of truth for the
ROCm version.
