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

# get device timing on sync clock using barcodes:
>>> recording_path = 's3://aind-ephys-data/ecephys_670248_2023-08-03_12-04-15/ecephys_clipped/Record Node 102/experiment1/recording1'
>>> sync_path = 's3://aind-ephys-data/ecephys_670248_2023-08-03_12-04-15/behavior/20230803T120415.h5'
>>> timing_data = next(npc_ephys.get_ephys_timing_on_sync(sync_path, recording_path))
>>> timing_data.device.name, timing_data.sampling_rate, timing_data.start_time
('Neuropix-PXI-100.ProbeA-AP', 30000.070518634246, 20.080209634424037)

# get a dataclass that reads SpikeInterface sorted data from the cloud
# - from a path:
>>> si = npc_ephys.get_spikeinterface_data('s3://codeocean-s3datasetsbucket-1u41qdg42ur9/4797cab2-9ea2-4747-8d15-5ba064837c1c')

# - or from a subject ID + date + session-index-on-date (separators are optional):
>>> si = npc_ephys.get_spikeinterface_data('670248_2023-08-03_0')

>>> si
SpikeInterfaceKS25Data(session='670248_2023-08-03_0', root=S3Path('s3://codeocean-s3datasetsbucket-1u41qdg42ur9/4797cab2-9ea2-4747-8d15-5ba064837c1c'))

# various bits of data are available for use:
>>> si.version
'0.97.1'
>>> ''.join(si.probes)
'ABCEF'
>>> si.quality_metrics_df('probeA').columns
Index(['num_spikes', 'firing_rate', 'presence_ratio', 'snr',
        'isi_violations_ratio', 'isi_violations_count', 'rp_contamination',
        'rp_violations', 'sliding_rp_violation', 'amplitude_cutoff',
        'drift_ptp', 'drift_std', 'drift_mad', 'isolation_distance', 'l_ratio',
        'd_prime'],
        dtype='object')
>>> si.spike_indexes('probeA')
array([      491,       738,       835, ..., 143124925, 143125165, 143125201])
>>> si.unit_indexes('probeA')
array([ 56,  61, 161, ..., 151,  72,  59])
```

# Development
See instructions in https://github.com/AllenInstitute/npc_ephys/CONTRIBUTING.md and the original template: https://github.com/AllenInstitute/copier-pdm-npc/blob/main/README.md