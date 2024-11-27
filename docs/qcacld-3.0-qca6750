# Enable Monitor Mode and Frame Injection on QCACLD-3.0

## Step 1: Load Appropriate Firmware

1. **Check Firmware Compatibility:**
    - Ensure the firmware supports monitor mode. Check the firmware files in `/lib/firmware/ath11k/qca6750/` or a similar location.
    - Common firmware files include:
        - `fw_image_1.0.1.0.816.3.bin`
        - `bdwlan.bin`

2. **Patch Firmware (Optional):**
    - Use tools like `hexedit` to modify flags in the binary.
    - Alternatively, search for community-patched firmware.

3. **Replace and Reload Firmware:**
    ```bash
    sudo cp /lib/firmware/ath11k/qca6750/fw_image*.bin /lib/firmware/ath11k/qca6750/fw_image_backup.bin
    sudo modprobe -r wlan
    sudo modprobe wlan
    ```

---

## Step 2: Enable Monitor Mode in the Driver

1. **Clone and Configure QCACLD-3.0:**
    ```bash
    git clone https://github.com/Codelinaro/qcacld-3.0.git
    cd qcacld-3.0
    ```
    Add the following to the configuration file (`config.ini` or similar):
    ```bash
    gEnableSuspendMon=1
    gEnableMonitorMode=1
    gEnableFrameInjection=1
    ```

2. **Compile and Install the Driver:**
    ```bash
    make defconfig
    make -j$(nproc)
    sudo make install
    sudo modprobe wlan
    ```

---

## Step 3: Activate Monitor Mode

1. **Check Available Interfaces:**
    ```bash
    iw dev
    ```

2. **Enable Monitor Mode:**
    ```bash
    sudo iw wlan0 set type monitor
    sudo ifconfig wlan0 up
    ```

3. **Verify Monitor Mode:**
    ```bash
    iw dev wlan0 info
    ```

---

## Step 4: Test Packet Injection

1. **Test with `aireplay-ng`:**
    ```bash
    aireplay-ng --test wlan0
    ```

2. **Modify Frame Injection Parameters:**
    - Ensure `HostARPOffload` and `HostNSOffload` are enabled in the driver.
    - Adjust parameters such as `skb_size` in the driver source code if necessary.

---

## Step 5: Verify with Aircrack-ng

1. **Check Interface with `airmon-ng`:**
    ```bash
    airmon-ng start wlan0
    ```

2. **Capture Packets with `airodump-ng`:**
    ```bash
    airodump-ng wlan0
    ```

---

> **Important:** Always ensure that you comply with local laws and regulations when using monitor mode and packet injection.

> **Note:** If issues persist, check debugfs entries at `/sys/kernel/debug/` and use dmesg logs to troubleshoot.
