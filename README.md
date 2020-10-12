# LineageOS device tree for the Samsung Galaxy J4

Description
-----------

This repository is to build LineageOS for the J4 (SM-J400M/F)

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

        m -j20 bacon
