## 如何编辑最小Intel Wi-Fi驱动程序？
#### 为了减少开机的启动时间，我们可能需要通过删除AirportItlwm.kext中的冗余固件来减小AirportItlwm.kext的大小。在本指南中，它将帮助您仅保留Intel WiFi卡使用的固件。
```shell
git clone --depth=1 https://github.com/OpenIntelWireless/itlwm.git
cd itlwm
git clone --depth=1 https://github.com/acidanthera/MacKernelSDK.git
```
<img src="/image/download.png" width="500">

#### 打开IORegistryExplorer应用程序，并搜索itlwm。在AirportItlwm下，检查IOModel属性中加载的固件。
<img src="/image/IOModel%20Property.png">

#### 导航到您的itlwm项目文件夹，并在itlwm项目文件夹中，仅保留与./itlwm/itlwm/firmware中IOModel属性匹配的固件。就我而言，我的wifi上加载的固件是iwlwifi-QuZ-a0-hr-b0-68.ucode，其中68是固件版本，可以根据itlwm版本而变化。
<img src="/image/firmware.png" width="400" align=left>
<img src="/image/delete_firmware.png" width="400" align=center>

#### 在终端应用程序中使用以下命令构建itlwm项目：
```shell
xcodebuild -scheme "AirportItlwm (all)" -configuration Release
```
<img src="/image/build.png" width="500">

#### 导航到~/Library/Developer/Xcode/DerivedData/itlwm-*/Build/Products/Release/*macOS Version*/AirportItlwm.kext。<br>AirportItlwm.kext的缩小大小应约为1.4 MB；将此构建AirportItlwm.kext复制到您的OpenCore Kexts文件夹中。启动时间应该减少一点。
<img src="/image/successful.png" width="500" align=center>
