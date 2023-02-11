# Running SONiC VS in GNS3 environment

NOTE: The instruction has been validated in fresh Ubuntu 20.04 environment.

## Install GNS3

Install GNS3:
```sh
sudo add-apt-repository ppa:gns3/ppa
sudo apt update
sudo apt install gns3-gui gns3-server
```

To be able to run GNS3 without root permissions, one additional step can be required:
```sh
sudo usermod -a -G ubridge $USER
```

.. then logout and login again.

For more information, please refer to GNS3 official documentation:
https://docs.gns3.com/docs/getting-started/installation/linux


## Install SONiC VS dependencies

Install SONiC VS dependencies:
```sh
sudo apt-get install libvirt-clients qemu-kvm libvirt-daemon-system
```

## Create GNS3 appliance for SONiC VS

Get SONiC VS image:
```sh
wget  'https://sonic-build.azurewebsites.net/api/sonic/artifacts?branchName=202205&platform=vs&buildId=205430&target=target%2Fsonic-vs.img.gz'  -O  sonic-vs.img.gz
gunzip sonic-vs.img.gz
```

Generate GNS3 appliance:
```sh
wget https://raw.githubusercontent.com/sonic-net/sonic-buildimage/202205/platform/vs/sonic-gns3a.sh
chmod +x sonic-gns3a.sh
./sonic-gns3a.sh -r 2205.1 -b sonic-vs.img
```

## Start SONiC VS topology in GNS3 environment

To start SONiC VS topology in GNS3 environment:
1. Import GNS3 SONiC appliance

2. Import sonic-l3-topo.gns3project portable project

3. Start topology

