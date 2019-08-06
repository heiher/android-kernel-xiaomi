# Android Kernel for XiaoMi

## How to build

### Toolchain
```bash
git clone --depth 1 https://github.com/heiher/aarch64-linux-android-4.9
export PATH=`pwd`/aarch64-linux-android-4.9/bin:${PATH}
```

### Xiaomi MAX 2 (oxygen)
```bash
git clone -b oxygen-n-oss --depth 1 https://github.com/heiher/android-kernel-xiaomi
cd android-kernel-xiaomi
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-android- oxygen_user_defconfig
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-android- Image.gz modules

git clone -b oxygen --depth 1 https://github.com/heiher/wlan-drivers-xiaomi
cd wlan-drivers-xiaomi
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-android- \
    -C`pwd`/../android-kernel-xiaomi WLAN_ROOT=`pwd` \
    MODNAME=wlan M=`pwd` CONFIG_PRONTO_WLAN=m modules
```

### Redmi Note 7 (lavender)
```bash
git clone -b lavender-p-oss --depth 1 https://github.com/heiher/android-kernel-xiaomi
cd android-kernel-xiaomi
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-android- lavender-perf_defconfig
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-android- Image.gz modules

git clone -b lavender --depth 1 https://github.com/heiher/wlan-drivers-xiaomi
git clone -b qca-wifi-host-cmn --depth 1 https://github.com/heiher/wlan-drivers-xiaomi qca-wifi-host-cmn
git clone -b fw-api --depth 1 https://github.com/heiher/wlan-drivers-xiaomi fw-api
cd wlan-drivers-xiaomi
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-android- \
    -C`pwd`/../android-kernel-xiaomi WLAN_ROOT=`pwd` \
    WLAN_COMMON_INC=`pwd`/../qca-wifi-host-cmn \
    WLAN_FW_INC=`pwd`/../fw-api MODNAME=wlan M=`pwd` \
    CONFIG_QCA_CLD_WLAN=m modules
```
