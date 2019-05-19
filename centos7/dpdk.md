## DPDK Minimal Setup
Download the DPDK latest LTS.tar.xz from [here](https://core.dpdk.org/download/).

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

### Remove (optional)
You need to remove current DPDK environment before you replace DPDK SDK with another release.
```
cd /home/dpdk-stable-18.11.1
make config T=x86_64-native-linuxapp-gcc
cd x86_64-native-linuxapp-gcc
make clean
rm -rf /usr/local/include/dpdk
cd /usr/local/lib
rm -rf libdpdk* librte*
cd /usr/local/bin
testpmd dpdk-procinfo dpdk-pdump dpdk-test-crypto-perf dpdk-test-eventdev dpdk-pmdinfo
rm /usr/local/sbin/dpdk-devbind
rm -rf /usr/local/lib/modules
rm /etc/sysconfig/modules/igb_uio.modules
rm -rf /usr/local/share/dpdk
reboot
```

### to be continued