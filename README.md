### 如何编辑最小Intel Wi-Fi驱动程序？
#### 为了减少开机的启动时间，我们可能需要通过删除AirportItlwm.kext中的冗余固件来减小AirportItlwm.kext的大小。在本指南中，它将帮助您仅保留Intel WiFi卡使用的固件。
```shell
git clone --depth=1 https://github.com/OpenIntelWireless/itlwm.git
cd itlwm
git clone --depth=1 https://github.com/acidanthera/MacKernelSDK.git
```
![图片](https://github.com/sunbos/AirportItlwm-minimize/blob/9196bcb27c821d9e83b24d2ecf7f348311205d67/image/download.png)
#### 打开IORegistryExplorer应用程序，并搜索itlwm。在AirportItlwm下，检查IOModel属性中加载的固件。
![图片](https://github.com/sunbos/AirportItlwm-minimize/blob/1483d612b88a9f4964af81f58c97be6665a948ea/image/IOModel%20Property.png)
#### 导航到您的itlwm项目文件夹，并在itlwm项目文件夹中，仅保留与./itlwm/itlwm/firmware中IOModel属性匹配的固件。就我而言，我的wifi上加载的固件是iwlwifi-QuZ-a0-hr-b0-68.ucode，其中68是固件版本，可以根据itlwm版本而变化。
![图片](https://github.com/sunbos/AirportItlwm-minimize/blob/34e5980801f451078ba4f504e556bb39977803b8/image/firmware.png)
#### 在终端应用程序中使用以下命令构建itlwm项目：
```shell
xcodebuild -scheme "AirportItlwm (all)" -configuration Release
```
#### 导航到~/Library/Developer/Xcode/DerivedData/itlwm-*/Build/Products/Release/*macOS Version*/AirportItlwm.kext。<br>AirportItlwm.kext的缩小大小应约为1.4 MB；将此构建AirportItlwm.kext复制到您的OpenCore Kexts文件夹中。启动时间应该减少一点。
![图片](https://github.com/sunbos/AirportItlwm-minimize/blob/e90f7b50b42d3920430116393bfa592c66cf1bac/image/release.png)
