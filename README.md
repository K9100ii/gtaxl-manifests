# Manifest for building LineageOS 20.0 for gtaxlwifi, gtaxllte, gtanotexlwifi, and gtanotexllte

`gtaxlwifi` is the codename for the WiFi-only variant of the Samsung Galaxy Tab A 10.1" (2016), with model SM-T580.

`gtaxllte` is the codename for the LTE variant of the Samsung Galaxy Tab A 10.1" (2016), with model SM-T585, and also with SM-T585N0 and SM-T585C for Korea and China respectively.

`gtanotexlwifi` is the codename for the WiFi-only variant of the Samsung Galaxy Tab A 10.1" (2016) **with S-Pen**, with model SM-P580, and also with SM-P583 for China.

`gtanotexllte` is the codename for the LTE variant of the Samsung Galaxy Tab A 10.1" (2016) **with S-Pen**, with models SM-P585, SM-P585M, SM-P585Y, SM-P585N0, and SM-P588C.

Some extremely basic instructions:

These assume you have a good Linux build environment prepared with all prerequisite dependencies installed. If not, you should be able to find out how to prepare a build environment, and what dependencies you should have installed for your specific Linux distribution, by searching elsewhere.

- Make a new directory for LineageOS 20.0 sources and enter it:
```
mkdir lineage-20.0
cd lineage-20.0
```

- Initialize repo in this directory with Lineage's android.git repository:
```
repo init -u https://github.com/LineageOS/android.git -b lineage-20.0 --git-lfs
```

- Clone this repository to .repo/local_manifests for the manifest, gtaxl.xml, containing the repositories needed to build for these devices:
```
git clone https://github.com/K9100ii/gtaxl-manifests.git -b lineage-20.0 .repo/local_manifests
```

- Sync all of the repositories in manifests (including LineageOS manifests):
```
repo sync --force-sync --no-tags --no-clone-bundle -c
```

- Forks from LineageOS repositories may become out-of-date from new changes until I (@K9100ii) get around to updating them again. Before building, you'll need to go through gtaxl.xml, and, for forks that have remove-project lines with names starting with "LineageOS/", update (rebase) them from upstream repositories. For example, for frameworks/base (note the second and third commands only need to be ran once per repository):
```
cd frameworks/base
git remote add lineage https://github.com/LineageOS/android_frameworks_base
git config pull.rebase true
git pull lineage lineage-20.0
cd ../..
```

- Finally, build as you like. For example, for a recovery-installable package for gtaxlwifi:
```
. build/envsetup.sh
lunch lineage_gtaxlwifi-userdebug
mka otapackage
```
