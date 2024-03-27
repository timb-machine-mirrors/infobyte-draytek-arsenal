# Draytek Arsenal: Observability and hardening toolset for Draytek edge devices.
Advanced attackers are increasingly choosing edge devices as targets. However, these devices are controlled by closed-source software known as firmware, often distributed in a proprietary format. This is an added difficulty for defenders and researchers, who must understand how to extract firmware to assess its security.

This is more than just a hypothetical scenario, as we discovered recently when a client was compromised. With Draytek equipment at the edge of their infrastructure, the natural question was: Could this be the attackers' entry point? Over 500k Draytek devices are exposed to the Internet. Yet, no working tool exists to extract their firmware and assist researchers and defenders working with these devices.

During our assessment, we reverse-engineered Draytek's firmware format, which contains a bootloader, a compressed RTOS kernel, and two filesystems. Through our investigation, we developed tools to extract these components, unveiling the real-time operating system's capability to load code modules dynamically. These modules are loaded from one of the filesystems in the firmware image during boot but can also be loaded while the system is running and stored in a separate filesystem in flash memory. An attacker can exploit this feature to achieve persistence by loading a module that remains active even after a reboot or firmware upgrade, and the end-user does not have a way to detect this type of attack. Consequently, we developed our own module to check the integrity of loaded modules in memory, mitigating this potential threat.

In our pursuit of a more secure internet, we are making this set of tools accessible to the community, enabling observability, hardening, transparency, and vulnerability research on Draytek edge devices

## Note
We initially developed this as a internal tool. Just as a set of scripts but showed great potential, prompting us to make it open source. Since then, we are working to integrate these scripts into the python package you will find in this repo, and to make them compatible with other device models.

## Get started ##

__Requirements:__

* python3
* Docker

### Installation ###

Build `mips-tools`:

```bash
$ cd mips-tools
$ docker build . -t mips-tools
```

Install `draytek_arsenal`:
```bash
$ cd draytek_arsenal
$ python3 -m pip install .
```

Test the installation:
```
$ python3 -m draytek_arsenal
```

### Install as developer ###

This installation will be affected by local code changes
```
$ python3 -m pip install -e .
```
