# Sionna-AcoustiX
[[arXiv](https://arxiv.org/abs/2411.06307)] [[Website](https://zitonglan.github.io/project/avr/avr.html)] [[AVR Code](https://github.com/penn-waves-lab/AVR)] [[BibTex](#citation)] 


This is an **acoustic impulse response simulation platform** based on the [Sionna](https://github.com/NVlabs/sionna) ray tracing engine. This is used by the [NeurIPS'24 Paper Acoustic Volume Rendering for Neural Impulse Response Fields.]((https://arxiv.org/abs/2411.06307))

This repo contains the Sionna ray tracing  engine, which is primarily for radio-frequency signal simulations. We modify the ray interactions with the environments to support Sionna for acosutic simulator and build **AcoustiX**.

We are still working on this repo to make it more user-friendly. Stay tuned!

# Updates
- 2025.12.15: We updated the liscence.
- 2025.03.04: we update the collect_dataset.py. With [detailed configuration files](#simulation-config-file)


# Contents
This repo contains the official implementation for AcoustiX.
- [Installation](#installation)
- [Structure](#project-structure)
- [Usage](#usage)
- [Config](#config)
- [Citation](#citation)


# Installation
* install the sionna ray tracing package (we have modifyed the source code on sionna to support acoustic simulation)
```sh
cd sionna
pip install .
```

# Project structure

```sh
AcoustiX/
├── extract_scene/              # tools to extract the scene files from igibson dataset      
├── img_render/                 # tools to extract the img from igibson dataset
├── simu_config/                # simulation config file
│   ├── basic_config.yml        # basic omnidirectional impulse response config        
│   └── directional_config.yml  # directional impulse response config
├── sionna/                     # sionna ray tracing engine
├── acoustic_absorptions.json   # common material configuration files   
├── ir_utils.py                 # ir metric utils
├── simu_utils.py               # simulation utils 
├── pattern.py                  # speaker or microphone gain pattern file
├── collect_dataset.py          # basic file to collect the impulse response dataset
├── README.md              # Project documentation
└── .gitignore             # Git ignore file
```


# Usage
### Minimim usage of AcoustiX to simulate impulse response
```sh
python3 collect_dataset.py --save-data # store data to a file 
python3 collect_dataset.py # just show the impulse response data
```

### Use iGibson dataset 
1. To use iGibson dataset for simulation, please go download the [iGibson dataset](https://svl.stanford.edu/igibson/)
2. Extract the scene files in the ./extrac_scene
```sh
python3 extract_scene.py # extract the environment ply files
python3 generate_xml.py # generate the AcoustiX simulator compatible files .XML
```

### Simulation config file
We refer the following configuration to simu_config/basic_config.yml

#### **Ray-Tracing Configuration (`rt_config`)**
| Entry        | Default Value | Description |
|-------------|--------------|-------------|
| `max_depth` | 10           | Maximum number of reflections for ray tracing. |
| `num_samples` | 50000      | Number of ray samples for Monte Carlo simulation. |
| `los`       | `true`       | Enable line-of-sight (direct path). |
| `reflection` | `true`      | Enable sound reflections. |
| `diffraction` | `false`     | Enable diffraction effects. |
| `scattering` | `true`      | Enable scattering effects. |
| `scat_prob` | 0.00001      | Probability of scattering occurring. |

#### **Impulse Response Configuration (`ir_config`)**
| Entry        | Default Value | Description |
|-------------|--------------|-------------|
| `attn`      | 0.001        | Attenuation factor for impulse response. |
| `fs`        | 48000        | Sampling frequency in Hz. |
| `ir_len`    | 4800         | Impulse response length in samples. |
| `speed`     | 343.8        | Speed of sound in m/s. |
| `noise`     | 0.001        | Noise level in impulse response. |
| `tx_pattern` | `uniform`   | Transmission pattern (e.g., `uniform`, `directional`). |
| `rx_pattern` | `uniform`   | Receiver pattern (e.g., `uniform`, `directional`). |


### Customized environments
To create your own acoustic environment, please go and check the official tutrial about Sionna: [Create your own scene using blender](https://www.youtube.com/watch?v=7xHLDxUaQ7c)

# Liscense
AcoustiX is licensed under a [MIT License](LICENSE).


# Citation
If you find this project to be useful for your research, please consider citing the paper.
```
@inproceedings{lanacoustic,
  title={Acoustic Volume Rendering for Neural Impulse Response Fields},
  author={Lan, Zitong and Zheng, Chenhao and Zheng, Zhiwei and Zhao, Mingmin},
  booktitle={The Thirty-eighth Annual Conference on Neural Information Processing Systems}
}
```
