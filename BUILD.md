### Use `Android-9.0`
```bash
repo init -u git://github.com/PitchBlackRecoveryProject/manifest_pb.git -b android-9.0 --depth=1
```

### Local manifest
```bash
mkdir -p .repo/local_manifests
curl -Ls https://gist.github.com/koumaza/a0682287a6703732f9b40157b53439e8/raw/05b5d3d2e39a43c16a66717f1941b45c787f9fb9/pbrb-payton.xml > .repo/local_manifests/pbrp-payton.xml
```

### Sync
```bash
repo sync -c -j$(($(nproc --all) * 24)) --force-sync --no-clone-bundle --no-tags
```

### Build
```bash
. build/envsetup.sh
lunch omni_$codename-eng
export ALLOW_MISSING_DEPENDENCIES=true
export cpuj=num
mkdir -p ~/log/$(pwd|tr / _|sed -E s/^_//) && mka bacon -j$(($(nproc --all) * $cpuj)) | tee ~/log/$(pwd|tr / _|sed -E s/^_//)/$(date +%Z_%m%d-%H:%M:%S.%N.log)
```
