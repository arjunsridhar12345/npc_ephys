# npc_ephys

Tools for accessing and processing raw ephys data, compatible with data in the cloud.

[![PyPI](https://img.shields.io/pypi/v/npc_ephys.svg?label=PyPI&color=blue)](https://pypi.org/project/npc_ephys/)
[![Python version](https://img.shields.io/pypi/pyversions/npc_ephys)](https://pypi.org/project/npc_ephys/)

[![Coverage](https://img.shields.io/codecov/c/github/AllenInstitute/npc_ephys?logo=codecov)](https://app.codecov.io/github/AllenInstitute/npc_ephys)
[![CI/CD](https://img.shields.io/github/actions/workflow/status/AllenInstitute/npc_ephys/publish.yml?label=CI/CD&logo=github)](https://github.com/AllenInstitute/npc_ephys/actions/workflows/publish.yml)
[![GitHub issues](https://img.shields.io/github/issues/AllenInstitute/npc_ephys?logo=github)](https://github.com/AllenInstitute/npc_ephys/issues)

# Usage
```bash
conda create -n npc_ephys python>=3.9
conda activate npc_ephys
pip install npc_ephys
```

## Windows
[`wavpack-numcodecs`](https://github.com/AllenNeuralDynamics/wavpack-numcodecs)
is used to read compressed ephys data from S3 (stored in Zarr format). On Windows, that requires C++
build tools to be installed: if `pip install npc_ephys` fails you'll likely need to download it [from here](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022).

## Python
```python
>>> import npc_ephys
```

# Development
See instructions in https://github.com/AllenInstitute/npc_ephys/CONTRIBUTING.md and the original template: https://github.com/AllenInstitute/copier-pdm-npc/blob/main/README.md