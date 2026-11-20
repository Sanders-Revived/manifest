# Sanders-Revived RisingOS Local Manifest

Local manifests and compatibility patches for building RisingOS Revived 9
(Android 17) on the Motorola Moto G5S Plus (`sanders`).

## Setup

1. Initialize the RisingOS source tree:

   ```bash
   repo init -u https://github.com/RisingOS-Revived/android -b seventeen --git-lfs
   ```

2. Clone this repository into the local-manifests directory:

   ```bash
   git clone -b rising-17 https://github.com/Sanders-Revived/manifest.git .repo/local_manifests
   ```

3. Sync the source tree:

   ```bash
   repo sync -c --no-clone-bundle --optimized-fetch --prune --force-sync -j"$(nproc --all)"
   ```

4. From the root of the source tree, apply the compatibility patches:

   ```bash
   for patch in $(find .repo/local_manifests -name '*.patch' | sort); do
       repo_path="${patch#.repo/local_manifests/}"
       repo_dir="${repo_path%/*}"
       git -C "$repo_dir" am "$PWD/$patch"
   done
   ```

   The patches add support for the separate recovery kernel configuration and
   device tree used by the `sanders` legacy boot image.

## Build

   ```bash
   . build/envsetup.sh
   riseup sanders user
   rise b
   ```
