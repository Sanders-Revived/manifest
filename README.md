# Sanders-Revived Local Manifests

This repository contains the local manifests for building LineageOS (or other AOSP-based ROMs) for the Motorola G5s Plus (sanders).

## How to use

1. Initialize your ROM source tree (e.g. LineageOS 23.2).
   ```bash
   repo init -u https://github.com/LineageOS/android.git -b lineage-23.2 --git-lfs --depth=1
   ```

2. Clone this manifest repository into `.repo/local_manifests`:
   ```bash
   git clone https://github.com/Sanders-Revived/manifest.git -b 16.0-4.19 .repo/local_manifests
   ```

3. Sync the repositories:
   ```bash
   repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
   ```

4. Apply all required patches:
   ```bash
   for patch in $(find .repo/local_manifests -name "*.patch" | sort); do git -C "$(dirname "${patch#.repo/local_manifests/}")" am "$PWD/$patch"; done
   ```
   *(Or individually)*:
   ```bash
   git -C build/make am "$PWD"/.repo/local_manifests/build/make/*.patch
   git -C vendor/lineage am "$PWD"/.repo/local_manifests/vendor/lineage/*.patch
   ```

5. Set up the build environment and start building!
   ```bash
   source build/envsetup.sh
   breakfast sanders
   brunch sanders
   ```
