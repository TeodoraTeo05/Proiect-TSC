# Proiect TSC 2025 - OpenBook

## 1. Diagrama bloc a sistemului

Diagrama bloc de mai jos ilustrează modul de interconectare al componentelor principale utilizate în cadrul proiectului:

![Block Diagram](https://docs.google.com/drawings/d/1UpxRyJNfczJHhNRvWdeb5kh_7IEUy5173odk93W_GSA/export/png)

## 2. Bill of Materials (BOM)

| Componentă           | Tip                                    | Link Achiziție (Mouser/Comet)                                                                 | Datasheet                                                                                     |
|------------------------|----------------------------------------|--------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| ESP32-C3-WROOM         | Microcontroller                        | [Mouser](https://www.mouser.com/ProductDetail/Espressif-Systems/ESP32-C3-WROOM-1-N8)            | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c3-wroom-1_datasheet_en.pdf) |
| MCP73832               | Battery Charger IC                     | [Mouser](https://www.mouser.com/ProductDetail/Microchip-Technology/MCP73832T-2ATI-OT)           | [Datasheet](https://ww1.microchip.com/downloads/en/devicedoc/22036b.pdf)                     |
| LDO 3.3V               | Low Dropout Regulator                  | [Comet](https://www.comet.ro/ro/ldo-voltage-regulators)                                          | Exemplu: [XC6220A331MR-G](https://datasheet.lcsc.com/lcsc/1811021613_Torex-Semiconductor-XC6220A331MR-G_C116416.pdf) |
| DC/DC Converter 5V     | Convertor Tensiune                     | [Mouser](https://www.mouser.com/c/power/dc-dc-converters/)                                      | Depinde de modelul ales                                                                      |
| E-Ink Display (1.5")    | Afișaj E-Paper                     | [Waveshare](https://www.waveshare.com/product/displays/e-paper/epaper-1.54inch.htm)             | [Datasheet](https://www.waveshare.com/wiki/1.54inch_e-Paper_Module)                          |
| SD Card Module         | Cititor microSD                        | [Comet](https://www.comet.ro/ro/sloturi-si-conectori-sd-microsd)                                | Model: 112A-TAAR-R03, [Datasheet](https://www.attend.com.tw/products-detail/112A-TAAR-R03)   |
| BME680                 | Temp/RH Sensor                         | [Mouser](https://www.mouser.com/ProductDetail/Bosch/BME680)                                    | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf) |
| MH-Z19B                | CO2 Sensor                             | [Mouser](https://www.mouser.com/ProductDetail/Winsen/MH-Z19B)                                   | [Datasheet](https://www.winsen-sensor.com/d/files/PDF/MH-Z19B.pdf)                          |
| PMSA003                | Particulate Matter Sensor (PM2.5)      | [Mouser](https://www.mouser.com/ProductDetail/Plantower/PMSA003)                               | [Datasheet](https://www.winsen-sensor.com/d/files/PDF/PMSA003.pdf)                          |
| Buttons                | Tactile Buttons                        | [Mouser](https://www.mouser.com/ProductDetail/Panasonic/EVQ-P7P01K)                             | [Datasheet](https://media.digikey.com/pdf/Data%20Sheets/Panasonic%20Electronic%20Components/EVQ-P7P01K_DS.pdf) |

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

