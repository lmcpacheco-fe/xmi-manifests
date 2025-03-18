# xmi-manifests
This is a repo for the XMI IMX8MP yocto platform, which is a part of the larger XMI project.
This project is based off work done for the Goldilocks platform, which was developed by Future's FIS team.

Note: This README assumes the user is running Ubuntu 22.04:

## Install required packages:
```
sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential \
chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils \
iputils-ping python3-git python3-jinja2 python3-subunit zstd liblz4-tool file \
locales libacl1
```

## Setup the repo utility:
```
mkdir ~/bin (this step may not be needed if the bin folder already exists)
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH && echo export PATH=~/bin:$PATH >> ~/.bashrc
```
## Configure Git:
```
git config --global user.name "Your Name"
git config --global user.email "Your Email"
git config --list
```
## Create the BSP directory and download the Yocto BSP:
```
mkdir ~/xmi-yocto-bsp
cd ~/xmi-yocto-bsp
repo init -u https://github.com/lmcpacheco-fe/xmi-manifests -b main -m xmi-manifest-6.6.23.xml
repo sync
```
## Create and configure the build folder:
```
MACHINE=xmi-imx8mp DISTRO=fsl-imx-xwayland source imx-setup-release.sh -b xmi-build
echo "BBLAYERS += \"\${BSPDIR}/sources/meta-xmi\"" >> conf/bblayers.conf
echo "LICENSE_FLAGS_ACCEPTED = \" commercial \""  >> conf/local.conf
```

## Build the XMI Linux image:
```
bitbake imx-image-multimedia
```
