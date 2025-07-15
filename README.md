https://github.com/ColdWindScholar/Auto-Twrp-Builder

# <div align="center">Build TWRP for your phone on GitHub with just one click by uploading your recovery!</div>

## Device Compatibility
- This tool works with most Android devices, including:
  - Qualcomm (QCOM) devices
  - MediaTek (MTK) devices
  - Samsung Exynos devices
- Supports various Android versions from 8.1 to 12.1
- The tool automatically detects and configures the necessary device tree based on your recovery image

## Usage:
### 1. Fork this repository
- Click the "Fork" button at the top right of this GitHub repository
- Wait for the forking process to complete

### 2. Unpack your recovery using bootimg or other unpacking tools
- Download your device's stock recovery.img
- Use tools like Android Image Kitchen, Magiskboot, or other bootimg tools to unpack the recovery image
- Locate the default.prop or prop.default file in the extracted contents
- Add the line `ro.product.first_api_level=(your Android SDK version)` to this file
  - For example: `ro.product.first_api_level=29` for Android 10
  - You can find your Android SDK version [here](https://developer.android.com/tools/releases/platforms)
- Repack the recovery image with the modified file

### 3. Upload the repacked recovery.img to this project
- Go to your forked repository
- Click "Add file" → "Upload files"
- Upload your modified recovery.img file
- Commit the changes
- View the file and click on it to get the "Raw" view
- Copy the direct URL to this raw file

### 4. Go to Actions, enter the direct link and TWRP version information
- Navigate to the "Actions" tab in your forked repository
- Select the "Recovery Build (Legacy)" workflow
- Click "Run workflow"
- Enter the direct URL to your recovery.img file
- Select the appropriate TWRP manifest branch based on your Android version:
  - Android 8.1: twrp-8.1
  - Android 9.0: twrp-9.0
  - Android 10: twrp-10.0
  - Android 11: twrp-11
  - Android 12/12.1: twrp-12.1
- Leave the build target as "recovery" (default)

### 5. Click Run to start the build process
- Click the green "Run workflow" button
- The build process will start automatically
- You can monitor the progress in the Actions tab

### 6. Download the compiled Recovery from Releases
- Once the build is complete, go to the "Releases" section of your repository
- You'll find a new release with your device name and build ID
- Download the recovery.img file or any other generated files
- Flash the recovery.img to your device using fastboot or other appropriate methods

## Notes for Specific SoC Types

### Qualcomm (QCOM) Devices
- For Qualcomm devices, the build script automatically extracts and configures the necessary device-specific information
- The tool handles Qualcomm-specific partitions and configurations during the build process
- If you encounter issues with Qualcomm devices, ensure your recovery.img is properly extracted and contains all necessary device information

### MediaTek (MTK) Devices
- MediaTek devices are supported but may require additional attention to the partition layout
- For MTK devices, ensure your recovery.img contains the complete kernel headers
- The tool will automatically detect MediaTek-specific configurations from your recovery image
- Some older MediaTek devices might require additional manual configuration in the device tree

### Samsung Exynos Devices
- Exynos devices are supported through the standard TWRP build process
- For Samsung devices, ensure the recovery.img contains the proper board configuration
- Samsung-specific features like encryption support are handled automatically
- For devices with secure boot, additional steps may be required after flashing the built recovery 