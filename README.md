# Spyder OnDemand Application

![Experimental](https://img.shields.io/badge/stability-experimental-orange.svg)

This repository contains a [Open OnDemand](https://openondemand.org/) Batch Connect application for launching
the Spyder Python IDE on an HPC cluster.

## Overview

This app enables users to run [Spyder](https://www.spyder-ide.org/) in a VNC-powered graphical session directly on a
compute node. It provides an interactive development environment with access to the full computational resources
of the selected partition.

## Key Features

- Launch Spyder with a graphical UI via Open OnDemand
- Use full CPU, memory, and GPU resources of a compute node
- Configure job parameters via a dynamic form
- Supports multiple partition profiles with varying limits

## Usage

To launch a session:

1. Select the desired partition.
2. Set the number of CPUs, memory per core, and optional GPU usage (where available).
3. Click **Launch** to start the session.
4. Once the session starts, connect via the "Launch Spyder" button.

## Partition Resource Limits

The table below summarizes the maximum allowed resources per partition:

| Partition            | Max CPUs | Max Hours | Max GPUs |
|----------------------|----------|-----------|----------|
| interactive          | 48       | 2         | 0        |
| express              | 48       | 2         | 0        |
| short                | 48       | 12        | 0        |
| pascalnodes          | 28       | 12        | 4        |
| pascalnodes-medium   | 28       | 48        | 4        |
| medium               | 48       | 50        | 0        |
| long                 | 48       | 150       | 0        |
| intel-dcb            | 24       | 150       | 0        |
| amd-hdr100           | 128      | 150       | 0        |
| largemem             | 24       | 50        | 0        |
| largemem-long        | 24       | 150       | 0        |
| amperenodes          | 128      | 12        | 2        |
| amperenodes-medium   | 128      | 48        | 2        |

⚠️ GPU selection is only available in the following partitions:  
`pascalnodes`, `pascalnodes-medium`, `amperenodes`, and `amperenodes-medium`.

## Files Included

| File                     | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `manifest.yml`           | Metadata for the application (name, category, description, etc.)            |
| `form.yml.erb`           | Configuration file that defines the user-facing form inputs                 |
| `form.js`                | JavaScript controlling dynamic form behavior (e.g., GPU field visibility)   |
| `template/script.sh.erb`| Shell script template that configures the session environment               |
| `icon.png`               | Application icon displayed in the OnDemand dashboard                        |

## Requirements

- Spyder must be installed in an accessible conda environment.
- The appropriate modules (e.g., `shared`, `rc-base`, `Anaconda3`) must be available on the system.
- Your cluster must support VNC sessions via Open OnDemand.

### Conda Setup

You must create a Spyder-ready conda environment with the below command.

This example requires the `Anaconda3/2023.07-2` module, but you may need to adjust it based on your cluster's available modules.

```bash
module load Anaconda3/2023.07-2
conda create -n spyder-env -c conda-forge spyder numpy scipy pandas matplotlib sympy cython
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
