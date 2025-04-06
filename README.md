# Proiect TSC 2025 – OpenBook

## Descriere generală

OpenBook este un dispozitiv portabil de tip e-book reader bazat pe ESP32-C6. Dispozitivul conține un ecran e-paper, butoane de control, senzor de mediu, ceas de timp real și posibilitate de alimentare de la baterie Li-Po, fiind gândit ca un sistem eficient energetic și scalabil.
---

#### 1 Diagramă bloc

![Diagramă bloc](https://raw.githubusercontent.com/TeodoraTeo05/proiect-TSC/main/Images/diagrama.png)

---
## 2 BOM (Bill of Materials)

| Part | Device | Datasheet |
|------|--------|-----------|
| CHG_LED | ADAFRUIT_LEDCHIP-LED0603 | [ADAFRUIT_LEDCHIP-LED0603](N/A) |
| SJ1 | SJ | [SJ](N/A) |
| EPD_C5 | EAGLE-LTSPICE_CC0402 | [EAGLE-LTSPICE_CC0402](N/A) |
| R3 | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| R1_PWRUSB | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| C4_USB | EAGLE-LTSPICE_CC0402 | [EAGLE-LTSPICE_CC0402](N/A) |
| C1, C2, C6, C8, C9, C10, C_DELAY | ESP32_WROVER_EAGLE-LTSPICE_CC0402 | [ESP32_WROVER_EAGLE-LTSPICE_CC0402](N/A) |
| C3 | RCL_CPOL-EUCT3528 | [RCL_CPOL-EUCT3528](N/A) |
| R1, R1_PINH, R1_PINH1, R2_PINH, R2_PINH1, R4, R5, R6, R7, R8, R9, R10, R_BOOT, R_CHANGE, R_CL1, R_RESET | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| C7 | ESP32_WROVER_EAGLE-LTSPICE_CC0402 | [ESP32_WROVER_EAGLE-LTSPICE_CC0402](N/A) |
| J4 | 112A-TAAR-R03_ATTEND | [112A-TAAR-R03_ATTEND](N/A) |
| R_CAPACITOR | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| C5 | ESP32_WROVER_EAGLE-LTSPICE_CC0402 | [ESP32_WROVER_EAGLE-LTSPICE_CC0402](N/A) |
| EPD_C6, EPD_C7, EPD_C8, EPD_C9, EPD_C10, EPD_C11, EPD_C12 | EAGLE-LTSPICE_CC0402 | [EAGLE-LTSPICE_CC0402](N/A) |
| EPD_C1, EPD_C2 | ESP32_WROVER_EAGLE-LTSPICE_CC0402 | [ESP32_WROVER_EAGLE-LTSPICE_CC0402](N/A) |
| R2 | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| R1_BAT | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| Q1, Q2 | ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7 | [ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7](N/A) |
| R2_BAT | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| C5_USB | EAGLE-LTSPICE_CC0402 | [EAGLE-LTSPICE_CC0402](N/A) |
| C1_BAT, C1_BAT1, C1_BAT2, C2_BAT | ESP32_WROVER_EAGLE-LTSPICE_CC0402 | [ESP32_WROVER_EAGLE-LTSPICE_CC0402](N/A) |
| C4 | ESP32_WROVER_EAGLE-LTSPICE_CC0402 | [ESP32_WROVER_EAGLE-LTSPICE_CC0402](N/A) |
| R2-USB, R2-USB1 | ESP32_WROVER_EAGLE-LTSPICE_RR0402 | [ESP32_WROVER_EAGLE-LTSPICE_RR0402](N/A) |
| L1 | 744043680IND_4828-WE-TPC_WRE | [744043680IND_4828-WE-TPC_WRE](N/A) |
| IC1 | BD5229G-TR | [BD5229G-TR](N/A) |
| SENSOR2 | ESP32_WROVER_BME680_BME680 | [ESP32_WROVER_BME680_BME680](N/A) |
| U$2 | BUTTON_CUSYOMV1 | [BUTTON_CUSYOMV1](N/A) |
| U$3 | BUTTON_CUSYOMV1 | [BUTTON_CUSYOMV1](N/A) |
| C10_SUPERCAP | CPH3225A | [CPH3225A](https://www.snapeda.com/parts/CPH3225A/Seiko+Instruments/view-part/?ref=snap) |
| U3 | DS3231SN# | [DS3231SN#](https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=snap) |
| U2 | ESP32-C6-WROOM-1-N8 | [ESP32-C6-WROOM-1-N8](N/A) |
| PFMF.050.1 | ESP32C6_VARISTORCN1812 | [ESP32C6_VARISTORCN1812](N/A) |
| D2, D7 | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0 | [ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0](N/A) |
| MCP73831 | ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831 | [ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831](N/A) |
| J1 | FH34SRJ-24S-0.5SH_99_ | [FH34SRJ-24S-0.5SH_99_](N/A) |
| U4 | MAX17048G+T10 | [MAX17048G+T10](https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=snap) |
| D3, D4, D5 | MBR0530 | [MBR0530](https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=snap) |
| D6, D8, D9, D10, D11, D12 | PGB1010603MR | [PGB1010603MR](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=snap) |
| J3 | QWIIC_CONNECTORJS-1MM | [QWIIC_CONNECTORJS-1MM](N/A) |
| U$1 | BUTTON_CUSYOMV1 | [BUTTON_CUSYOMV1](N/A) |
| J2 | SAMACSYS_PARTS_USB4110-GF-A | [SAMACSYS_PARTS_USB4110-GF-A](N/A) |
| Q3 | SI1308EDL-T1-GE3 | [SI1308EDL-T1-GE3](N/A) |
| TP1, TP2, TP3, TP4, TP5, TP6, TP7, TP8, TP9, TP10, TP11, TP12, TP13, TP14, TP15, TP16, TP17 | TPTP20R | [facut de mine] |
| D1 | USBLC6-2SC6Y | [USBLC6-2SC6Y](https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=snap) |
| U1 | W25Q512JVEIQ | [W25Q512JVEIQ](https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=snap) |
| IC4 | XC6220A331MR-G | [XC6220A331MR-G](N/A) |

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

