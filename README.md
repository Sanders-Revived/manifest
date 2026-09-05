# Sanders-Revived Local Manifests

This repository contains the local manifests for building LineageOS (or other AOSP-based ROMs) for the Motorola G5s Plus (sanders).

## How to use

1. Initialize your ROM source tree (e.g. LineageOS 22.2).
   ```bash
   repo init -u https://github.com/LineageOS/android.git -b lineage-22.2 --git-lfs --depth=1
   ```

2. Clone this manifest repository into `.repo/local_manifests`:
   ```bash
   git clone https://github.com/Sanders-Revived/manifest.git .repo/local_manifests
   ```

3. Sync the repositories:
   ```bash
   repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
   ```

4. Set up the build environment and start building!
   ```bash
   source build/envsetup.sh
   breakfast sanders
   brunch sanders
   ```

