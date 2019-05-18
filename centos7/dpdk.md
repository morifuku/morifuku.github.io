## DPDK Minimal Setup
Download DPDK latest LTS.tar.gz from [here](https://core.dpdk.org/download/).

### Download, Make
```
yum install make gcc kernel-devel numactl-devel kernel-headers.x86_64 kernel.x86_64 wget pciutils
yum install kernel-devel-`uname -r`
cd /home
wget https://fast.dpdk.org/rel/dpdk-18.11.1.tar.xz
tar xJvf dpdk-18.11.1.tar.xz
cd dpdk-stable-18.11.1
make install T=x86_64-native-linuxapp-gcc DESTDIR=/usr/local EXTRA_CFLAGS="-O3 -g3"
```