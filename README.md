# LineageOS device tree for the Samsung Galaxy J4

Description
-----------

This repository is to build LineageOS for the J4 (SM-J400M/F)
## Spec Sheet

| Feature                 | Specification                     |
| :---------------------- | :-------------------------------- |
| CPU                     | Quad-core 1.4 GHz Cortex-A53      |
| Chipset                 | Exynos 7570                       |
| GPU                     | Mali-T720 MP2                     |
| Memory                  | 2GB	                              |
| Shipped Android Version | 8.1.0                             |
| Storage                 | 16 GB                             |
| MicroSD                 | Up to 256 GB                      |
| Battery                 | 3000 mAh (removable)              |
| Dimensions              | 151.7 x 77.2 x 8.1 mm             |
| Display                 | 720 x 1280 pixels,5.5(~267 PPI)     |
| Rear Camera             | 13 MP, LED flash                  |
| Front Camera            | 5 MP                              |
| Release Date            | May 2018                          |

## Device Picture

![Galaxy J4](https://prods.tugadgetshop.com/350/samsung-galaxy-j4-color-negro-frontal.jpg) 

How to build LineageOS
----------------------

* Make a workspace:

        mkdir -p ~/lineageos/repo
        cd ~/lineageos/repo

* Initialize the repo:

        repo init -u git://github.com/LineageOS/android.git -b lineage-17.1

* Create a local manifest:

        vim .repo/local_manifests/roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <project name="blackwidowroms/android_device_samsung_j4ltejx" path="device/samsung/j4ltejx" />
            <project name="blackwidowroms/android_device_samsung_exynos7570-common" path="device/samsung/exynos7570-common" remote="github" />
            <project name="blackwidowroms/android_kernel_samsung_exynos7570" path="kernel/samsung/exynos7570" remote="github" />
            <project name="blackwidowroms/android_vendor_samsung_7570" path="vendor/samsung/j4ltejx" remote="github" />
            <project name="LineageOS/android_device_samsung_slsi_sepolicy" path="device/samsung_slsi/sepolicy" remote="github" />
	    <project name="LineageOS/android_hardware_samsung" path="hardware/samsung" remote="github" />
        </manifest>

* Sync the repo:

        repo sync

* Extract vendor blobs

        cd device/samsung/j4ltejx
        ./extract-files.sh

* Setup the environment

        source build/envsetup.sh
        lunch lineage_j4ltejx-userdebug

* Build LineageOS

        m -j20 j4ltejx
