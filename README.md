# Manifest for building LineageOS 18.1 for gtaxlwifi and gtanotexlwifi

`gtaxlwifi` is the codename for the WiFi-only variant of the Samsung Galaxy Tab A 10.1" (2016), with model SM-T580.

`gtanotexlwifi` is the codename for the WiFi-only variant of the Samsung Galaxy Tab A 10.1" (2016) **with S-Pen**, with model SM-P580.

Some extremely basic instructions:
- Make a new directory for LineageOS sources and enter it:
```
mkdir lineage-18.1
cd lineage-18.1
```

- Initialize repo in this directory with the LineageOS 18.1 android repository:
```
repo init -u https://github.com/LineageOS/android.git -b lineage-18.1
```

- Clone this repository to .repo/local_manifests for roomservice.xml containing the repositories needed to build for these devices:
```
git clone https://github.com/TALUAtGitHub/gtaxlwifi-manifests.git -b lineage-18.1 .repo/local_manifests
```

- Sync all of the repositories in manifests (including LineageOS manifests):
```
repo sync --force-sync --no-tags --no-clone-bundle -c
```

- Finally, build as you like. For example, for a recovery-installable package for gtaxlwifi:
```
. build/envsetup.sh
lunch lineage_gtaxlwifi-userdebug
mka otapackage
```
...or for gtanotexlwifi:
```
. build/envsetup.sh
lunch lineage_gtanotexlwifi-userdebug
mka otapackage
```
