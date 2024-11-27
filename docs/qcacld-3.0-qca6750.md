## qca6750/wcn6750 devuce-tree configuration (dts)

```bash
    wifi: wifi@17a10040 {
        compatible = "qcom,wcn6750-wifi";
        reg = <0x17a10040 0x0>;
        iommus = <&apps_smmu 0x1c00 0x1>;
        interrupts = <GIC_SPI 768 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 769 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 770 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 771 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 772 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 773 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 774 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 775 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 776 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 777 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 778 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 779 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 780 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 781 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 782 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 783 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 784 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 785 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 786 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 787 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 788 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 789 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 790 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 791 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 792 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 793 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 794 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 795 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 796 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 797 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 798 IRQ_TYPE_EDGE_RISING>,
                     <GIC_SPI 799 IRQ_TYPE_EDGE_RISING>;
        qcom,rproc = <&remoteproc_wpss>;
        memory-region = <&wlan_fw_mem>, <&wlan_ce_mem>;
        qcom,smem-states = <&wlan_smp2p_out 0>;
        qcom,smem-state-names = "wlan-smp2p-out";
        wifi-firmware {
            iommus = <&apps_smmu 0x1c02 0x1>;
        };
    };
```

# Device Tree Node: `wifi@17a10040`

This Device Tree (DT) snippet describes the `wifi` node for a Qualcomm WCN6750 Wi-Fi module.

---

## Key Properties

### `compatible`
- Specifies the hardware compatibility string.  
  **Value:** `"qcom,wcn6750-wifi"`

### `reg`
- Defines the physical address or offsets for the device.  
  **Value:** `<0x17a10040 0x0>` (base address)

### `iommus`
- Links the device to the IOMMU (Input/Output Memory Management Unit).  
  **Value:** `<&apps_smmu 0x1c00 0x1>`  
  - `&apps_smmu`: Reference to the IOMMU node.
  - `0x1c00`: IOMMU Stream ID.
  - `0x1`: Context Bank ID.

### `interrupts`
- Declares 32 General Interrupt Controller (GIC) SPI interrupt lines.  
  Each is configured as edge-triggered.  
  **Values:** `<GIC_SPI 768 IRQ_TYPE_EDGE_RISING>` to `<GIC_SPI 799 IRQ_TYPE_EDGE_RISING>`  
  Likely used for events such as communication errors, packet processing, or control signals.

### `qcom,rproc`
- Links the Wi-Fi module to a remote processor (`remoteproc`) node.  
  **Value:** `<&remoteproc_wpss>` (associated remote processor)

### `memory-region`
- Points to memory regions reserved for Wi-Fi firmware and data:  
  - `<&wlan_fw_mem>`: Firmware memory region.
  - `<&wlan_ce_mem>`: Communication Engine (CE) memory for data transfers.

### `qcom,smem-states` & `qcom,smem-state-names`
- Configure shared memory (SMEM) state.  
  **Values:**  
  - `qcom,smem-states`: `<&wlan_smp2p_out 0>`  
  - `qcom,smem-state-names`: `"wlan-smp2p-out"`

### `wifi-firmware`
- A sub-node for handling IOMMU settings specific to the firmware.  
  **Value:** `<&apps_smmu 0x1c02 0x1>`  
  - Additional IOMMU details for firmware operations.

---

## Purpose

This node configures the WCN6750 Wi-Fi subsystem, ensuring proper integration with the SoC's:
- Interrupt infrastructure
- IOMMU
- Remote processor
- Memory architecture

It supports communication between the application processor and the Wi-Fi subsystem.

---

## Observations and Suggestions

1. **Interrupts:**
   - Ensure all 32 interrupts are required; if not, optimize by defining only the used lines.

2. **Memory Regions:**
   - Verify that `wlan_fw_mem` and `wlan_ce_mem` sizes and attributes align with hardware documentation.

3. **SMEM States:**
   - Confirm that `wlan_smp2p_out` is correctly linked to the shared memory node.

4. **Testing:**
   - Validate this configuration using kernel logs (`dmesg`) to ensure proper initialization.


# Firmware

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
