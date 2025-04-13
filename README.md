# Block Diagram
![Block Diagram](BLOCK_DIAGRAM.png)


# Hardware Features – Detailed Description

## 1. Microcontroller – ESP32-C6

- **Processor:** 32-bit RISC-V core, clocked up to 160 MHz.
- **Memory:** 512KB internal SRAM and 8MB external flash memory (model W25Q512JVEIQ).
- **Connectivity:** Supports Wi-Fi 6 (802.11ax), Bluetooth Low Energy 5, and USB 2.0 (full-speed).
- **Interfaces:** SPI, I²C, UART, and multiple available GPIOs.
- **Power Efficiency:** Power-saving modes, including deep sleep.

## 2. E-Paper Display – 7.5”

- **Model:** Waveshare or equivalent, with a resolution of 800×480 pixels.
- **Connection:** 4-wire SPI plus control pins (CS, DC, RST, BUSY).
- **Power Consumption:** Very low in static mode; during refresh, consumption ranges between 15–25mA.


## 3. Environmental Sensor – BME688

- **Measurements:** Temperature, relative humidity, atmospheric pressure, and air quality (eCO2/VOC).
- **Interface:** I²C protocol at 400kHz (SDA/SCL).
- **Power Consumption:** Approx. 2.1µA in standby, with peaks of a few mA when active.


## 4. Power Supply and Management System

- **Battery:** Li-Po 3.7V, 2500mAh capacity.
- **Charging:** MCP73831 – simple and reliable IC for USB-C charging, up to 1A.
- **Monitoring:** MAX17048 – fuel gauge providing voltage and battery level data.
- **Voltage Regulation:** LDO such as XC6220A331MR-G, for a stable 3.3V output.

**Why these components?**
- MCP73831 offers a compact and efficient solution.
- MAX17048 enables precise battery monitoring and low-level warnings.

## 5. Buttons – 3 units

- **Type:** Tactile switch (Panasonic or similar).
- **Purpose:** Menu navigation, page turning, option selection.
- **Connection:** To GPIOs, with hardware (RC) or software debouncing.

## 6. USB-C Connector

- **Purpose:** Power/charging + data transfer via USB 2.0.
- **Protection:** ESD (e.g., USBLC6-2SC6Y) and termination resistors.
- **Options:** Supports firmware updates via USB or OTA via Wi-Fi.

## 7. Qwiic Interface (I²C)

- **Pins:** VCC, GND, SDA, SCL.
- **Functionality:** Quick expansion with additional I²C sensors/modules.

## 8. SD Card Slot – 112A-TAAR-R03

- **Purpose:** Storing e-books, logs, or firmware files.
- **Connection:** SPI or SDIO, depending on implementation.

## 9. Real-Time Clock – DS3231

- **Purpose:** Precise timekeeping, even without main power.
- **Communication:** I²C (shared with other sensors).
- **Backup:** Supercapacitor or secondary battery.

## 10. Additional Memory

- **Model:** W25Q512JVEIQ – external flash memory.
- **Connection:** Dedicated SPI (quad SPI) for firmware and large files.

---

# 4. ESP32-C6 Pin Allocation

| ESP32-C6 Pin | Signal                        | Detailed                                   |
|--------------|-------------------------------|--------------------------------------------|
| GPIO1        | I²C SDA                       | Data line for sensors and RTC              |
| GPIO2        | I²C SCL                       | Clock line for I²C interface               |
| GPIO5        | SPI MISO                      | Data input from e-paper                    |
| GPIO6        | SPI MOSI                      | Data output to e-paper                     |
| GPIO7        | SPI CLK                       | Clock signal for SPI                       |
| GPIO8        | SPI CS (e-paper)              | Chip select for display                    |
| GPIO9        | E-paper DC                    | Switch between data and command modes      |
| GPIO10       | E-paper RST                   | Hardware reset for the display             |
| GPIO11       | E-paper BUSY                  | Status signal (busy/free)                  |
| GPIO12       | Button 1                      | Digital input for NEXT                     |
| GPIO13       | Button 2                      | Digital input for PREV                     |
| GPIO14       | Button 3                      | Digital input for OK/MENU                  |
| GPIO15       | MAX17048 ALERT (optional)     | Low battery alert                          |
| GPIO16       | USB D+                        | USB data line (fixed pin)                  |
| GPIO17       | USB D-                        | USB data line (fixed pin)                  |
| GPIO18       | Status LED (optional)         | Visual indicator for various states        |
| GPIO19       | SD Card CS                    | Chip select for SD card (SPI)              |
| GPIO20       | SD Card MISO                  | Data received from SD card                 |
| GPIO21       | SD Card MOSI                  | Data sent to SD card                       |
| GPIO4        | SD Card CLK                   | SPI clock line for SD communication        |

---

# Power Consumption Estimate

| Module                | Typical Consumption              |
|------------------------|----------------------------------|
| ESP32-C6 active        | ~80mA with Wi-Fi / <10mA idle   |
| E-paper (refresh)      | 15–25mA                         |
| BME688 active          | up to 3.6mA / 2.1µA standby     |
| MAX17048               | Approx. 50µA                    |
| DS3231                 | ~3.5mA active / <1µA backup     |
| MCP73831               | Varies based on charging current|

**Usage Scenarios:**
- In **deep sleep**, total consumption can drop below 100µA.
- In active mode with Wi-Fi and screen refresh, consumption may reach 100–150mA.
- A 2500mAh battery allows for **weeks of operation** in predominantly passive mode (static display, infrequent Wi-Fi activity).

---


# Bill of Materials:

| Component | Type | Marketplace | Datasheet |
|----------|------|-------------|-----------|
| EAGLE-LTSPICE_CC0402 | Capacitor | [Link](https://eu.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=ulEaXIWI0c9ebKRT3r3htg%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf) |
| ESP32_WROVER_EAGLE-LTSPICE_RR0402 | Resistor | [Link](https://eu.mouser.com/ProductDetail/Vishay-Beyschlag/MCS04020D9101BE000?qs=sGAEpiMZZMvdGkrng054twKDKoBh%252BscnK%2FuqkNk9X%252BqO%2Fz5%2F0u93Ow%3D%3D) | [Datasheet](https://www.vishay.com/docs/28700/mcx0x0xpre.pdf) |
| RCL_CPOL-EUCT3528 | Capacitor | [Link](https://eu.mouser.com/ProductDetail/Nichicon/LGN2W101MELA25?qs=Fe64Qgzkstf1zMszMsgRoA%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/293/e_lgn-3082370.pdf) |
| ADAFRUIT_LEDCHIP-LED0603 | LED | [Link](https://eu.mouser.com/ProductDetail/ams-OSRAM/KG-EELP41.22-PHRH-35-A8J8-20-R18?qs=ZcfC38r4Posajg8ZvCDQkg%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/588/KG_EELP41_22_EN-3572852.pdf) |
| CPH3225A | Capacitor | [Link](https://eu.mouser.com/ProductDetail/Seiko-Semiconductors/CPH3225A?qs=3etwrb1wR%252BhUOph6lAO7eg%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/360/Seiko_Instruments_MicroBattery_E_20230330_2024Jan_-3561061.pdf) |
| ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7 | Transistor | [Link](https://eu.mouser.com/ProductDetail/Diodes-Incorporated/DMG2305UX-7?qs=L1DZKBg7t5F%2FNBHrjfxC%252Bg%3D%3D) | [Datasheet](https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf) |
| ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0 | Diode | [Link](https://eu.mouser.com/ProductDetail/ROHM-Semiconductor/SCS310AMC7G?qs=iLKYxzqNS75xiccEgNnX2g%3D%3D) | [Datasheet](https://fscdn.rohm.com/en/products/databook/datasheet/discrete/sic/sbd/scs310am-e.pdf) |
| SI1308EDL-T1-GE3 | Transistor | [Link](https://eu.mouser.com/ProductDetail/Vishay-Semiconductors/SI1308EDL-T1-GE3?qs=bX1%252BNvsK%2FBramh9tgpOaEw%3D%3D) | [Datasheet](https://www.vishay.com/docs/63399/si1308edl.pdf) |
| ESP32C6_VARISTORCN1812 | Varistor | [Link](https://eu.mouser.com/ProductDetail/Schurter/PFMF.050.2?qs=1auRipcfynCums5v1iucSA%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/358/typ_PFMF-1275918.pdf) |
| ESP32_WROVER_BME680_BME680 | Integrated Environmental Unit | [Link](https://eu.mouser.com/ProductDetail/M5Stack/U001-C?qs=e8oIoAS2J1R2mB7ZY1%252BSZg%3D%3D) | [Datasheet](https://docs.m5stack.com/en/unit/envIII) |
| ESP32-C6-WROOM-1-N8 | MicroController | [Link](https://eu.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6?qs=Imq1NPwxi75noDtUpuVuWw%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/891/esp32_c6_datasheet_en-3304070.pdf) |
| 744043680IND_4828-WE-TPC_WRE | Inductor | [Link](https://eu.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D) | [Datasheet](https://www.we-online.com/components/products/datasheet/744043680.pdf) |
| SI1308EDL-T1-GE3 | Transistor | [Link](https://eu.mouser.com/ProductDetail/Vishay-Semiconductors/SI1308EDL-T1-GE3?qs=bX1%252BNvsK%2FBramh9tgpOaEw%3D%3D) | [Datasheet](https://www.vishay.com/docs/63399/si1308edl.pdf) |
| BD5229G-TR | Voltage Detector | [Link](https://eu.mouser.com/ProductDetail/ROHM-Semiconductor/BD5229G-TR?qs=sGAEpiMZZMutXGli8Ay4kAMqIQqqdOUlDFcDfPDPIK4%3D) | [Datasheet](https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf) |
| DS3231SN# | RTC Module | [Link](https://eu.mouser.com/ProductDetail/Analog-Devices-Maxim-Integrated/DS3231SN?qs=1eQvB6Dk1vhUlr8%2FOrV0Fw%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/609/DS3231-3421123.pdf) |
| USBLC6-2SC6Y | ESD Protection | [Link](https://eu.mouser.com/ProductDetail/STMicroelectronics/USBLC6-2SC6Y?qs=gNDSiZmRJS%2FOgDexvXkdow%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/389/usblc6_2sc6y-1852505.pdf) |
| W25Q512JVEIQ | Flash Memory | [Link](https://eu.mouser.com/ProductDetail/Winbond/W25Q512JVEIQ?qs=l7cgNqFNU1jw6svr3at6tA%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/949/Winbond_W25Q512JV_Datasheet-3240039.pdf) |
| SAMACSYS_PARTS_USB4110-GF-A | USB Connector | [Link](https://eu.mouser.com/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/837/GCT_USB4110_Product_Drawing___20k_cycles-3455479.pdf) |
| FH34SRJ | E-Paper Display Header | [Link](https://eu.mouser.com/ProductDetail/Hirose-Connector/FH34SRJ-7S-0.5SH50?qs=vcbW%252B4%252BSTIqHa4IamMh36g%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/185/FH34SRJ_7S_0_5SH_50__CL0580_1200_0_50_2DDrawing_00-1615127.pdf) |
| MAX17048G+T10 | Battery Management | [Link](https://eu.mouser.com/ProductDetail/Analog-Devices-Maxim-Integrated/MAX17048G%2bT10?qs=D7PJwyCwLAoGnnn8jEPRBQ%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/609/MAX17048_MAX17049-3469099.pdf) |
| MCP73831 | Battery Controller | [Link](https://eu.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ATI-MC?qs=yUQqVecv4qs9k7ug0bEXiw%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/268/MCP73831_Family_Data_Sheet_DS20001984H-3441711.pdf) |
| 112A-TAAR-R03_ATTEND | SD Card Mount | [Link](https://store.comet.srl.ro/Catalogue/Product/43497/) | [Datasheet](https://store.comet.srl.ro/Catalogue/Product/43497/) |
| XC6220A331MR-G | LDO Voltage Regulator | [Link](https://eu.mouser.com/ProductDetail/Torex-Semiconductor/XC6220A331MR-G?qs=AsjdqWjXhJ8ZSWznL1J0gg%3D%3D) | [Datasheet](https://eu.mouser.com/datasheet/2/760/xc6220-3371556.pdf) |

