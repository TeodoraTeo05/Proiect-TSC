fa diagrama bloc alba si nu folosi emoticoane!
fa l putin mai lung, te poti inspira si de aici, dar nu l face la fel!:## Horia Mercan - OpenBook - Systems Testing

This project presents the electronic design (schematic/pcb) and the visual design of a complete ebook. 


## Hardware Modules and Components

**ESP32-C6-WROOM-1-N8 – Main Microcontroller:**
* Power Supply: 3.3V.
* Communications: SPI, I2C, UART, GPIO.

We will link interfaces of each module with main controller's pins:

**SPI ESD Protection Lines**
* Protects the SPI lines for the SD card, e-paper, external flash.

**LDO Voltage Regulator**
* Steps down the voltage from 5V to 3.3V to power the ESP32-C6 and other modules.

**SD Card Module**
* Interface: SPI
* Pins Used:
    * `SS_SD` → `IO4`
    * `MOSI` → `IO7`
    * `MISO` → `IO2`
    * `SCK` → `IO6`

**E-Paper Display**
* Interface: SPI
* Pins Used:
    * `EPD_CS` → `IO10`
    * `EPD_DC` → `IO5`
    * `EPD_RST` → `IO23`
    * `EPD_BUSY` → `IO3`
    * `MOSI`, `SCK` (shared with SD)

**RTC Module - DS3231SN**
* Interface: I2C
* Pins Used:
    * `SCL` → `IO22`
    * `SDA` → `IO21`
    * `INT_RTC` → `IO8`
    * `32KHZ` → `IO1`
    * `RTC_RST` → `IO18`

**LiPo Fuel Gauger**
* Built-in charging control.
* MAX17048G+T10
* Battery level monitoring with:
    * Battery ChargeLevel IC → I2C => `SDA`, `SCL`

**Qwiic / Stemma QT Connector**
* Communicates entirely via I2C: `SCL`/`SDA` 

**Environmental Sensor - BME688**
* Protocol: I2C (shared) => `SDA`, `SCL`



**Environmental Sensor - BME688**
* Interface: I2C (shared with RTC)
* Power Supply: 3.3V
* Pins Used:  `SDA`, `SCL`

**External Flash - NORFlash64MB**
* Interface: SPI
* Pins Used:
    * `FLASH_CS` → `IO11`
    * Rest (`MOSI`, `MISO`, `SCK`) shared

**SD/USB interface**
* `USB_D+` → `IO13`
* `USB_D-` → `IO12`

**Reset and Boot Buttons**
* `IO/BOOT` → `IO9`
* `RESET` → `EN`


**Diodes for reverse polarity protection.**

**USB-C Connector + ESD Protection**
* Main power and data input.
* Includes TVS diodes for ESD protection.



## Block components & schematic

![Block functionalities and components for OpenBook](./Images/Schema%20OpenBook.png)


## Communication Interfaces

| Interface | Connected Components       | ESP32-C6 Pins                       |
| :-------- | :------------------------- | :------------------------------------ |
| SPI       | SD Card, E-paper, NOR Flash | `MOSI` (`IO7`), `MISO` (`IO2`), `SCK` (`IO6`) |
| I2C       | RTC, BME688, Battery Level | `SDA` (`IO22`), `SCL` (`IO21`)        |
| UART      | Debugging / Flash          | `TX` (`GPIO16`), `RX` (`GPIO17`)        |
| GPIO      | Buttons, status signals    | `IO0` - `IO23`                        |
| USB       | PC connection / power      | `USB_D+`/`D-` (`IO13`/`IO12`)

## Energy management

| Component                   | Power Supply (V) | Estimated Current (mA) | Estimated Power (W) | Notes                                                                  |
|-----------------------------|-------------------|------------------------|----------------------|------------------------------------------------------------------------|
| ESP32-C6-WROOM-1-N8         | 3.3               | 150 (average)          | 0.5                  | Active mode; varies significantly based on usage.                       |
| SD Card Module              | 3.3               | 10 (average)           | 0.033                | Intermittent read/write operations.                                     |
| E-Paper Display             | 3.3               | 1(average)             | 0.0033               | Power used only during updates, very low average.                   |
| RTC Module - DS3231SN       | 3.3               | 1                      | 0.0033               |                                                                        |
| LiPo Fuel Gauger (MAX17048) | 3.3               | 0.05                   | 0.000165             | Very low power consumption.                                            |
| BME688 (Environmental Sensor) | 3.3               | 1 (average)            | 0.0033               | Intermittent readings.                                                  |
| NORFlash64MB (External Flash)| 3.3               | 2 (average)            | 0.0066               | Intermittent read/write operations.                                     |
| LDO Voltage Regulator       | 5 (input) / 3.3 (output) | Variable             | Variable               | Efficiency depends on load; quiescent current is very low.             |
| USB-C Connector + ESD       | 5 (input)         | Variable               | Variable               | Power depends on charging current; ESD protection negligible.          |
| Reset/Boot Buttons          | N/A               | Negligible             | Negligible           |                                                                        |
| **Total (Approximate)** |                   |          150-200              | **~0.55** | This is a rough estimate; actual power depends on duty cycles and usage. |

## Images

![Device](./Images/dispozitiv_1.PNG)
![PCB](./Images/placa_1.png)

# BOM

| Piece Name | Piece Type | Link |
|------------|------------|------|
| SAMACSYS_PARTS_USB4110-GF-A | USB-C Connector | https://www.snapeda.com/parts/USB4110-GF-A./Global%20Connector%20Technology/view-part/ |
| ESP32_WROVER_EAGLE-LTSPICE_R | Resistor | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO |
| MAX17048G+T10 | Cell Fuel Gauge | https://www.snapeda.com/parts/MAX17048G+T10/Analog%20Devices/view-part/ |
| W25Q512JVEIQ | Flash Memory (NOR) | https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond%20Electronics/view-part/?ref=search&t=W25Q512JVEIQ |
| RCL_CPOL-EU | Polarized Capacitor | https://grabcad.com/library/tantalum-smd-capacitor-type-b-3528-1 |
| ESP32-C6-WROOM-1-N8 | ESP32 Module | https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif%20Systems/view-part/?ref=search&t=ESP32-C6-WROOM-1-N8 |
| ADAFRUIT_CHIP-LED0603 | LED | https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/view-part/?ref=search&t=LED%200603 |
| ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831 | Li-Ion/Li-Poly Charge Management Controller | https://componentsearchengine.com/part-view/MCP73831T-2ACI%2FOT/Microchip |
| ESP32_WROVER_BME680_BME680 | Environmental Sensor | https://www.snapeda.com/parts/BME680/Bosch%20Sensortec/view-part/?ref=search&t=bme680 |
| CPH3225A | Crystal | https://www.snapeda.com/parts/CPH3225A/Seiko/view-part/ |
| BUTTON_CUSYOMV1 | Button | https://ro.mouser.com/ProductDetail/Panasonic/EVQ-P7L01P?qs=rJ%252BziJWpyszWhhNszc02jQ%3D%3D&utm_id=6470900573&utm_source=google&utm_medium=cpc&utm_marketing_tactic=emeacorp&gad_source=1&gbraid=0AAAAADn_wf2u1-1FzOTFyljDC4WPsSKtJ&gclid=Cj0KCQjwqcO_BhDaARIsACz62vPVeStXn6lXkpk-IPhYAE7F2gpbfTm751cNxrlbJa5xGxG5NT01Z4waAqXEEALw_wcB&_gl=1*bly5rh*_ga*NDU0NzEyMTQxLjE3NDM4Nzk4OTU.*_ga_15W4STQT4T*MTc0Mzg4MTg0Ni4yLjAuMTc0Mzg4MTg0Ny41OS4wLjA. |
| FH34SRJ-24S-0.5SH_99_ | FPC Connector | https://componentsearchengine.com/part-view/FH34SRJ-24S-0.5SH(99)/Hirose |
| 744043680 | Inductor | https://eu.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D |
| PGB1010603MR | TVS Diode (0603) | https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/ |
| SJ | 3-Way Solder Jumper | https://grabcad.com/library/solder-jumpers-1 |
| XC6220A331MR-G | Voltage Regulator | https://ro.mouser.com/ProductDetail/Torex-Semiconductor/XC6220A331MR-G?qs=AsjdqWjXhJ8ZSWznL1J0gg%3D%3D&utm_source=octopart&utm_medium=aggregator&utm_campaign=865-XC6220A331MR-G&utm_content=Torex%20Semiconductor |
| QWIIC_CONNECTOR | I²C Connector (PRT-14417) | https://www.snapeda.com/parts/PRT-14417/SparkFun/view-part/ |
| ESP32-CAP C0402 | Capacitor | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO |
| ESP VARSISTOR | Varistor (B72520T0350K062) | https://ro.mouser.com/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D |
| MBR0530 | Schottky Diode | https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/ |
| ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH | MOSFET (DMG2305UX-7) | https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated |
| 112ATAARR03 | microSD | https://www.snapeda.com/parts/112A-TAAR-R03/Attend/view-part/ |
| ESP32_WROVER_AVX---SD0805S020S1R0 | Schottky Diode | https://componentsearchengine.com/part-view/SD0805S020S1R0/Kyocera%20AVX |
| DS3231SN# | I²C-Integrated RTC/TCXO/Crystal | https://www.snapeda.com/parts/DS3231SN%23/Analog%20Devices/view-part/?ref=search&t=DS3231SN%23 |
| BD5229G-TR | Voltage Detector | https://www.snapeda.com/parts/BD5229G-TR/Rohm/view-part/?ref=search&t=BD5229G-TR |
| SI1308EDL-T1-GE3 | MOSFET Transistor | https://www.snapeda.com/parts/SI1308EDL-T1-GE3/Vishay/view-part/ |
| TP | Test Pad | none |
| USBLC6-2SC6Y | TVS Diode | https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=dk&t=USBLC6-2SC6Y&con_ref=None |
