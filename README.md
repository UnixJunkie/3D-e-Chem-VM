# 3D e-Chem Virtual Machine

[![Build Status](https://travis-ci.org/3D-e-Chem/3D-e-Chem-VM.svg?branch=master)](https://travis-ci.org/3D-e-Chem/3D-e-Chem-VM)
[![DOI](https://zenodo.org/badge/19641/3D-e-Chem/3D-e-Chem-VM.svg)](https://zenodo.org/badge/latestdoi/19641/3D-e-Chem/3D-e-Chem-VM)

Scripts to create a Vagrant box using packer and ansible.

For available software/datasets/workflows inside Virtual machine see https://github.com/3D-e-Chem/3D-e-Chem-VM/wiki

# Usage

* VirtualBox, https://www.virtualbox.org
* Vagrant, https://www.vagrantup.com

Start virtual machine with

```
vagrant init nlesc/3d-e-chem
vagrant up
```

# Build

Requirements:

* Virtualbox, https://www.virtualbox.org/
* Packer, https://packer.io
* Enough disk space
  * Make sure temporary directory (/tmp by default on Linux) has enough space. Use TMPDIR environment variable to overwrite default location
* ova file `../Chemical-Analytics-Platform/output-virtualbox-iso/cap.ova` from build phase of https://github.com/NLeSC/Chemical-Analytics-Platform

```
packer build packer.json
```
# Test

Add box to Vagrant with

```
vagrant box remove --force --all nlesc/3d-e-chem
vagrant box add --name nlesc/3d-e-chem --force packer_virtualbox-ovf_virtualbox.box
```

Then use steps described at Usage chapter in a new directory.

# Push

Requirements:

* Atlas account, https://atlas.hashicorp.com

Publish box on https://atlas.hashicorp.com/nlesc/boxes/3d-e-chem using the following steps:

1. Create a new version
2. Create a new provider
3. Choose `virtualbox` as provider
4. Choose Upload
5. Press `Continue to upload`
6. Upload the `packer_virtualbox-ivf_virtualbox.box` file generated by `vagrant package`
7. Edit version
8. Press `Release version`

# Contributing

Please see [CONTRIBUTING.md](CONTRIBUTING.md).
