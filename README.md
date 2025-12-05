# Spyder Open OnDemand Application

![Experimental](https://img.shields.io/badge/stability-experimental-blue.svg)

This repository contains a [Open OnDemand](https://openondemand.org/) Batch Connect application for launching
the Spyder Python IDE on an HPC cluster.

⚠️ This has now been adapted by [UAB Research Computing](https://rc.uab.edu/) for use on the [Cheaha cluster](https://docs.rc.uab.edu/cheaha/). The app is located at: <https://gitlab.rc.uab.edu/rc-data-science/community-ood-sandbox/spyderide>.

## Overview

This app enables users to run [Spyder](https://www.spyder-ide.org/) in a VNC-powered graphical session directly on a
compute node. It provides an interactive development environment with access to the full computational resources
of the selected partition.

I was motivated to create this as an alternative to using remote tunneling via code-server.

The following examples were very useful:

- [UAB RC's Examples](https://gitlab.rc.uab.edu/rc-data-science/community-ood-sandbox)
- [SupercomputingWales Example Spyder App](https://github.com/SupercomputingWales/scw_ood_spyder)

## Key Features

- Launch Spyder with a graphical UI via Open OnDemand
- Use full CPU, memory, and GPU resources of a compute node
- Configure job parameters via a dynamic form
- Supports multiple partition profiles with varying limits

## Usage

1. Users must set up the OOD Sandbox using instructions from the [Cheaha Open OnDemand documentation](https://docs.rc.uab.edu/workflow_solutions/creating_sandbox_apps/#setting-up-ood-sandbox-for-your-cheaha-account).

    ⚠️ If you are not using the Cheaha cluster, you may need to follow different steps.

2. Users must clone an existing OOD app using [these instructions](https://docs.rc.uab.edu/workflow_solutions/creating_sandbox_apps/#fsl).

3. Instead of using the FSL app, users should clone this repository: `git@github.com:sdhutchins/ood-spyder.git`

### Launching Spyder

To launch a session:

1. Select the desired partition.
2. Set the number of CPUs, memory per core (recommended to use at least 8 GB total), and optional GPU usage (where available).
3. Click **Launch** to start the session.
4. Once the session starts, connect via the "Launch Spyder" button.

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
