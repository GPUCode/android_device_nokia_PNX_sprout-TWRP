# Device Tree for Nokia 8.1

The Nokia 8.1, also known as the Nokia X7 in China, is a Nokia-branded mid-range smartphone by HMD Global. It was announced on 6 December 2018.

| Basic                   | Spec Sheet                                                                                                                     |
| -----------------------:|:------------------------------------------------------------------------------------------------------------------------------ |
| CPU                     | Octa-core (2x2.2 GHz 360 Gold & 6x1.7 GHz Kryo 360 Silver)                                                                           |
| Chipset                 | Qualcomm SDM710 Snapdragon 710 (10 nm)                                                                                                 |
| GPU                     | Adreno 616                                                                                                                     |
| Memory                  | 4/6 GB RAM                                                                                                                     |
| Shipped Android Version | Android 9.0                                                                                                                            |
| Last Android Version    | Android 11                                                                                                                            |
| Storage                 | 64/128 GB                                                                                                                          |
| Battery                 | Li-Ion 3500 mAh, non-removable                                                                                        |
| Display                 | 1080 x 2280 pixels, 19:9 ratio (~408 ppi density)                                                                              |
| Camera (Back)           | 12 MP, f/1.8, 1/2.55", 1.4µm, dual pixel PDAF, OIS                                                                              |
| Camera (Front)          | 20 MP, f/2.0, (wide), 1/3", 0.9µm                                                                                                    |

## Device picture

![Nokia 8.1](https://images.ctfassets.net/wcfotm6rrl7u/GU6kG7ai70GSfz6k9Geh1/8075b893d1888e7a58015e5c3a6bc36c/nokia-8_1-plus-blue_silver-front_back-int.png?h=1000&fm=webp)

## Compile

First repo init the TWRP 10.0 tree (and necessary qcom dependencies):

```
mkdir ~/android/twrp-10.0
cd ~/android/twrp-10.0
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-10.0
mkdir -p .repo/local_manifests
curl https://raw.githubusercontent.com/TeamWin/buildtree_manifests/master/min-omni-10.0/qcom.xml > .repo/local_manifests/qcom.xml
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="GPUCode/android_device_nokia_PNX_sprout-TWRP" path="device/nokia/PNX_sprout" remote="github" revision="android-10"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the twrp installer, you need to import this commit in the build/make path: https://gerrit.omnirom.org/#/c/android_build/+/33182/

Finally execute these:

```
. build/envsetup.sh
export LC_ALL=C
lunch omni_NB1-eng
mka adbd recoveryimage
```