# ROCm SDK for Workshop

An AMD GPU runtime and development toolkit. It installs ROCm from the official
AMD APT repository on Ubuntu 22.04 and 24.04, and from the Ubuntu archive on
Ubuntu 26.04, typically alongside a language SDK for GPU-accelerated workloads.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: gpu-workload
base: ubuntu@24.04
sdks:
  - name: uv
    channel: 0.9/stable
  - name: rocm
    channel: 7.1/stable

actions:
  check-gpu: |
    rocminfo
```

This demonstrates GPU access verification inside a workshop with both a
language SDK and the ROCm companion runtime.

---

## Using the SDK

### Prerequisites, project layout

The SDK installs the complete ROCm GPU compute development and system toolset
and automatically configures environment paths.

| Base           | Source                    | Default packages     | Install prefix |
| -------------- | ------------------------- | -------------------- | -------------- |
| `ubuntu@22.04` | AMD APT repository        | `rocm-dev`           | `/opt/rocm`    |
| `ubuntu@24.04` | AMD APT repository        | `rocm-dev`           | `/opt/rocm`    |
| `ubuntu@26.04` | Ubuntu archive (ROCm 7.1) | `rocm-dev rocm-smi g++` | `/usr`      |

On `ubuntu@26.04` the ROCm packages come from the Ubuntu archive, so the
installed ROCm version follows the archive rather than the SDK channel; use
the `7.1` track there.

To build a project in the workshop:

```bash
git clone git@github.com:ROCm/rocm-examples.git
workshop launch
workshop shell
make
```

### Verify GPU access

Once the workshop is ready:

```bash
workshop shell
rocminfo
```

This lists detected AMD GPUs and their capabilities. For a monitoring view:

```bash
rocm-smi
```

---

## Plugs (resources this SDK consumes)

### `gpu`

- Interface: `gpu`
- Purpose: Grants access to AMD GPU hardware on the host.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [ROCm official documentation](https://rocm.docs.amd.com/)
- [Workshop documentation](https://ubuntu.com/workshop/docs/)

---

## Community and support

- ROCm community: [ROCm GitHub](https://github.com/ROCm/ROCm)
- Workshop forum:
  [Discourse](https://discourse.ubuntu.com/)
- Please review our
  [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct) before
  participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See `CONTRIBUTING.md` for guidelines.
- Open issues or pull requests on the official repository.

---

## License and copyright

Copyright 2025 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under
the terms of the
[GNU Lesser General Public License version 2.1 (LGPLv2.1)](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html)
as published by the Free Software Foundation.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

[ROCm](https://github.com/ROCm/ROCm) is licensed under the
[MIT License](https://opensource.org/licenses/MIT).
