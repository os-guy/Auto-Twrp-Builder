# Auto-TWRP Builder

<p align="center">
  <img src="https://twrp.me/images/twrp-logo.png" alt="TWRP Logo" width="300"/>
</p>

<h2 align="center">Build TWRP for your phone on GitHub with just one click by uploading your recovery!</h2>

> [!NOTE]
> This tool supports most Android devices and automatically generates a device tree based on your recovery image.

## 📱 Device Compatibility

This tool works with most Android devices, including:

- **Qualcomm (QCOM)** devices
- **MediaTek (MTK)** devices
- **Samsung Exynos** devices

Supports various Android versions from 8.1 to 12.1. The tool automatically detects and configures the necessary device tree based on your recovery image.

## 🚀 Usage Guide

### 1. Fork this repository

- Click the "Fork" button at the top right of this GitHub repository
- Wait for the forking process to complete

### 2. Prepare your recovery image

1. Download your device's stock recovery.img
2. Use tools like Android Image Kitchen, Magiskboot, or other bootimg tools to unpack the recovery image
3. Locate the `default.prop` or `prop.default` file in the extracted contents
4. Add the line `ro.product.first_api_level=(your Android SDK version)` to this file
   - For example: `ro.product.first_api_level=29` for Android 10
   - You can find your Android SDK version [here](https://developer.android.com/tools/releases/platforms)
5. Repack the recovery image with the modified file

> [!IMPORTANT]
> Adding the correct Android SDK version is critical for proper device detection and configuration.

### 3. Upload the recovery image

1. Go to your forked repository
2. Click "Add file" → "Upload files"
3. Upload your modified recovery.img file
4. Commit the changes
5. View the file and click on it to get the "Raw" view
6. Copy the direct URL to this raw file

### 4. Start the build process

1. Navigate to the "Actions" tab in your forked repository
2. Select the "Recovery Build" workflow
3. Click "Run workflow"
4. Enter the direct URL to your recovery.img file
5. Select the appropriate TWRP manifest branch based on your Android version:

   | Android Version | TWRP Branch |
   |-----------------|-------------|
   | Android 8.1     | twrp-8.1    |
   | Android 9.0     | twrp-9.0    |
   | Android 10      | twrp-10.0   |
   | Android 11      | twrp-11     |
   | Android 12/12.1 | twrp-12.1   |

6. Leave the build target as "recovery" (default)
7. Click the green "Run workflow" button
8. The build process will start automatically
9. You can monitor the progress in the Actions tab

> [!TIP]
> The build process may take 15-30 minutes depending on GitHub's runner availability and your device complexity.

### 5. Download your custom TWRP

- Once the build is complete, go to the "Releases" section of your repository
- You'll find a new release with your device name and build ID
- Download the recovery.img file or any other generated files
- Flash the recovery.img to your device using fastboot or other appropriate methods

> [!WARNING]
> Always back up your current recovery before flashing a custom one. Incorrect flashing can lead to a bricked device.

## ℹ️ Notes for Specific SoC Types

### Qualcomm (QCOM) Devices

> [!NOTE]
> For Qualcomm devices, the build script automatically extracts and configures the necessary device-specific information. The tool handles Qualcomm-specific partitions and configurations during the build process.
>
> If you encounter issues with Qualcomm devices, ensure your recovery.img is properly extracted and contains all necessary device information.

### MediaTek (MTK) Devices

> [!NOTE]
> MediaTek devices are supported but may require additional attention to the partition layout. For MTK devices, ensure your recovery.img contains the complete kernel headers.
>
> The tool will automatically detect MediaTek-specific configurations from your recovery image. Some older MediaTek devices might require additional manual configuration in the device tree.

### Samsung Exynos Devices

> [!NOTE]
> Exynos devices are supported through the standard TWRP build process. For Samsung devices, ensure the recovery.img contains the proper board configuration.
>
> Samsung-specific features like encryption support are handled automatically. For devices with secure boot, additional steps may be required after flashing the built recovery.

## 🔧 Troubleshooting

> [!TIP]
> If you encounter issues during the build process:
>
> 1. Check the build logs in the Actions tab for specific errors
> 2. Ensure your recovery.img is properly unpacked and repacked
> 3. Verify that you've added the correct Android SDK version to the properties file
> 4. Try using a different TWRP branch version that might be more compatible with your device

> [!CAUTION]
> If the build fails with errors related to missing dependencies, this usually indicates that your device requires specific proprietary blobs or configurations that weren't detected automatically. 