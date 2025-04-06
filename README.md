# Proiect TSC 2025 - OpenBook

## 1. Diagrama bloc a sistemului

Diagrama bloc de mai jos ilustrează modul de interconectare al componentelor principale utilizate în cadrul proiectului:

![Block Diagram](https://docs.google.com/drawings/d/1UpxRyJNfczJHhNRvWdeb5kh_7IEUy5173odk93W_GSA/export/png)

## BOM (Bill of Materials)

| Component | Value | Description | Datasheet | Purchase Link |
|-----------|-------|-------------|-----------|----------------|
| CHG_LED | - | LED | - | - |
| SJ1 | - | SMD solder JUMPER | - | - |
| EPD_C5 | 0.1uF/50V | CAPACITOR, European symbol | - | - |
| R3 | 0.47 | RESISTOR, European symbol | - | - |
| R1_PWRUSB | 100k | RESISTOR, European symbol | - | - |
| C4_USB | 100nF | CAPACITOR, European symbol | - | - |
| C1, C2, C6, C8, C9, C10, C_DELAY | 100nF | CAPACITOR, European symbol | - | - |
| C3 | 100uF TANT | POLARIZED CAPACITOR, European symbol | - | - |
| R1, R1_PINH, R1_PINH1, R2_PINH, R2_PINH1, R4, R5, R6, R7, R8, R9, R10, R_BOOT, R_CHANGE, R_CL1, R_RESET | 10k | RESISTOR, European symbol | - | - |
| C7 | 10uF | CAPACITOR, European symbol | - | - |
| J4 | 112A-TAAR-R03_ATTEND | Micro SD Card Socket, Push-Push Type, Top Mount, SMT, H=1.83mm, 10u | - | - |
| R_CAPACITOR | 15 | RESISTOR, European symbol | - | - |
| C5 | 1uF | CAPACITOR, European symbol | - | - |
| EPD_C6, EPD_C7, EPD_C8, EPD_C9, EPD_C10, EPD_C11, EPD_C12 | 1uF/50V | CAPACITOR, European symbol | - | - |
| EPD_C1, EPD_C2 | 1uF/50V | CAPACITOR, European symbol | - | - |
| R2 | 2.2 | RESISTOR, European symbol | - | - |
| R1_BAT | 200 | RESISTOR, European symbol | - | - |
| Q1, Q2 | 20V/4.2A/52mΩ/1.4W | P-channel MOSFETs | - | - |
| R2_BAT | 2k | RESISTOR, European symbol | - | - |
| C5_USB | 4.7uF | CAPACITOR, European symbol | - | - |
| C1_BAT, C1_BAT1, C1_BAT2, C2_BAT | 4.7uF | CAPACITOR, European symbol | - | - |
| U4 | MAX17048G+T10 | Battery Fuel Gauge | [Datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/MAX17048-MAX17049.pdf) | [Mouser](https://www.mouser.com/ProductDetail/Maxim-Integrated/MAX17048G-T10) |
| U2 | ESP32-C6-WROOM-1-N8 | ESP32 WiFi+BT SoC | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_datasheet_en.pdf) | [Mouser](https://www.mouser.com/ProductDetail/Espressif/ESP32-C6-WROOM-1-N8) |
| U3 | DS3231SN# | RTC (Real Time Clock) | [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS3231.pdf) | [Mouser](https://www.mouser.com/ProductDetail/Maxim-Integrated/DS3231SN) |
| SENSOR2 | BME688 | Environmental Sensor | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme688-ds000.pdf) | [Mouser](https://www.mouser.com/ProductDetail/Bosch-Sensortec/BME688) |

## 3. Funcționalitate hardware

Proiectul OpenBook este un cititor de tip e-paper, alimentat din baterie LiPo și construit în jurul microcontrollerului ESP32-C3-WROOM. 
Dispozitivul colectează date de mediu (temperatură, umiditate, CO2, particule), le salvează pe card microSD și le poate afișa pe ecranul e-paper.

### ESP32-C3-WROOM
- Modulul principal cu conectivitate Wi-Fi/BLE, capabil să comunice prin SPI, I2C și UART.
- Tensiune de alimentare: 3.3V, furnizată de LDO.

### Sistem de alimentare
- **USB-C** este utilizat pentru încărcare și comunicare USB.
- **MCP73832** gestionează încărcarea bateriei LiPo.
- **LDO 3.3V** alimentează ESP32 și restul componentelor la 3.3V.
- **DC/DC 5V** generează 5V pentru senzorii care necesită tensiune mai mare (PM și CO2).

### Senzori
- **BME680** - senzor de temperatură, umiditate și gaze, comunică prin I2C.
- **MH-Z19B** - senzor de CO2 alimentat la 5V, comunică prin UART.
- **PMSA003** - senzor pentru particule fine (PM2.5), comunică prin UART, 5V.

### Afișaj
- Display e-paper monocrom de 1.5" cu rezoluție 200x200 px.
- Interfață SPI comună cu SD Card-ul.

### SD Card
- Modul pentru stocarea datelor colectate sau a fișierelor text.
- Interfață SPI.

### Butoane
- 3 butoane tactile conectate la GPIO pentru control interfață (ex. navigare meniu, refresh ecran).

### Calcule de consum estimativ (valori medii)

| Modul                | Tensiune | Curent (mA) | Consum estimativ |
|----------------------|----------|-------------|------------------|
| ESP32-C3             | 3.3V     | 80-150       | 0.3-0.5W         |
| E-Ink Display        | 3.3V     | 10 (refresh) | 0.03W            |
| BME680               | 3.3V     | 2-3          | 0.01W            |
| MH-Z19B              | 5V       | 40-50        | 0.25W            |
| PMSA003              | 5V       | 60-100       | 0.5W             |
| SD Card              | 3.3V     | 10           | 0.03W            |
| MCP73832 (charger)   | 5V       | 1000 (max)   | doar când încarcă |

**Modul deep sleep:** Consum sub 1 mA total. Ideal pentru dispozitiv portabil.

## 4. Pinout ESP32-C3

| Pin ESP32-C3     | Componentă                 | Motiv / Semnal                          |
|------------------|------------------------------|-----------------------------------------|
| GPIO1 (I2C SDA)  | BME680                       | Comunicație I2C                       |
| GPIO2 (I2C SCL)  | BME680                       | Comunicație I2C                       |
| GPIO3 (UART RX)  | PMSA003                      | UART RX senzor PM                       |
| GPIO4 (SPI CS SD)| SD Card                      | Chip Select SD Card                     |
| GPIO5            | E-Ink DC                     | Date/Command E-Ink                      |
| GPIO6 (SPI CLK)  | E-Ink & SD                   | Clock SPI                              |
| GPIO7 (SPI MOSI) | E-Ink & SD                   | Date SPI                               |
| GPIO8 (GPIO)     | Buton 1                      | Control meniu / page flip              |
| GPIO9 (GPIO)     | Buton 2                      | Control meniu / page flip              |
| GPIO10 (SPI CS)  | E-Ink Display                | Chip Select e-paper                    |
| GPIO11 (SPI CS)  | Flash extern (opțional)     | N/A                                    |
| GPIO12 (USB D-)  | USB                          | Comunicație USB                       |
| GPIO13 (USB D+)  | USB                          | Comunicație USB                       |
| GPIO18           | MH-Z19B (UART TX)            | UART pentru senzor CO2                 |
| GPIO19           | Buton 3                      | Navigare / confirmare                  |

## 5. Alte aspecte relevante

- Designul PCB respectă recomandările de trasee de putere (min 0.3mm), semnale (min 0.15mm).
- Antena ESP32-C3 este amplasată spre exteriorul plăcii, iar zona de sub ea este decupată.
- Condensatoarele de decuplare sunt apropiate de VCC-ul componentelor.
- Plan de masă solid pe ambele layere și via stitching activ.
- Toate componentele pasive sunt SMD 0402.
- Layout-ul este proiectat în Fusion360, aliniat cu dimensiunile carcasei fizice.
- Imaginile randate ale dispozitivului și carcasei se găsesc în folderul `Images/` din acest repository.

