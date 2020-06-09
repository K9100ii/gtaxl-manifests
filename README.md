# Manifest for building LineageOS for the Samsung Galaxy Tab A 10.1" (2016), codenamed gtaxlwifi

Make a new directory for LineageOS sources:
```
mkdir lineage-17.1
cd lineage-17.1
```

Initialize repo in this directory with the LineageOS 17.1 android repository:
```
repo init -u https://github.com/LineageOS/android.git -b lineage-17.1
```

Clone this repository to .repo/local_manifests for roomservice.xml containing the repositories needed to build for this device:
```
git clone https://github.com/TALUAtGitHub/gtaxlwifi-manifests.git -b lineage-17.1 .repo/local_manifests
```

Sync all of the repositories in manifests (including LineageOS manifests):
```
repo sync --force-sync --no-tags --no-clone-bundle -c
```

Finally, build as you like. For example, for a recovery-installable package:
```
. build/envsetup.sh
lunch lineage_gtaxlwifi-userdebug
mka otapackage
```
