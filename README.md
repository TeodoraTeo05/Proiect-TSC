# OpenBook - Proiect TSC 2025

## 1. Diagramă bloc

Diagrama bloc completă este disponibilă aici: [Diagrama Bloc - Google Drawings](https://docs.google.com/drawings/d/1UpxRyJNfczJHhNRvWdeb5kh_7IEUy5173odk93W_GSA/edit?usp=sharing)

Aceasta ilustrează conexiunile dintre ESP32-C6-WROOM-1, modulele de alimentare, senzori, afișajul e-paper, butoanele fizice, portul USB-C, memoria flash externă, RTC-ul și cititorul de card microSD.

---

## 2. BOM - Bill of Materials

| Componentă                    | Tip                       | Link achiziție                                                                                 | Datasheet                                                                                  |
|-------------------------------|----------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| ESP32-C6-WROOM-1-N8          | Microcontroller            | [Mouser](https://www.mouser.com/ProductDetail/356-ESP32C6WROOM1N8)                              | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6_datasheet_en.pdf) |
| MCP73831                     | Controller încărcare baterie | [Mouser](https://www.mouser.com/ProductDetail/579-MCP73831T-2ACIOT)                            | [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/20001984g.pdf)               |
| MAX17048                     | Fuel Gauge baterie         | [Mouser](https://www.mouser.com/ProductDetail/700-MAX17048GT10)                                | [Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX17048.pdf)                    |
| DS3231SN                     | Ceas RTC                   | [Mouser](https://www.mouser.com/ProductDetail/913-DS3231SN)                                    | [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS3231.pdf)                      |
| BME688                       | Senzor de mediu            | [Comet](https://www.comet.ro/bme688)                                                            | [Datasheet](https://www.bosch-sensortec.com/products/environmental-sensors/gas-sensors/bme688/) |
| 7.5" E-Ink Display (WSH-13187) | Afișaj e-paper           | [Waveshare](https://www.waveshare.com/wiki/7.5inch_e-Paper_V2)                                 | [Datasheet](https://www.waveshare.com/w/upload/e/e8/7.5inch-e-paper-v2-specification.pdf)   |
| 112A-TAAR-R03                | Slot card microSD          | [Comet](https://store.comet.srl.ro/Catalogue/Product/43497/)                                  | [Datasheet](https://www.attend.com.tw/uploads/product/file/20210105/112A-TAAR-R03.pdf)     |
| USB4110-GF-A                | Conector USB-C             | [Mouser](https://www.mouser.com/ProductDetail/GCT/USB4110-GF-A)                               | [Datasheet](https://gct.co/files/drawings/usb4110.pdf)                                     |
| LDO XC6220                  | Regulator tensiune 3.3V    | [Mouser](https://www.mouser.com/ProductDetail/865-XC6220A331MR-G)                             | [Datasheet](https://www.torexsemi.com/file/xc6220/XC6220.pdf)                             |
| Butoane tactice             | Comutatoare SMD            | [Mouser](https://www.mouser.com/ProductDetail/667-EVQPUJ02K)                                  | [Datasheet](https://industrial.panasonic.com/cdbs/www-data/pdf/ATK0000/ATK0000C144.pdf)     |
| Rezistențe 0402           | Pasive SMD                 | [Mouser](https://www.mouser.com/ProductDetail/YAGEO/RC0402FR-0710KL)                          | [Datasheet](https://www.yageo.com/upload/media/product/productSeries/15/Yageo-RC-Series-Datasheet-2022.pdf) |

---

## 3. Descriere hardware completă

### ESP32-C6-WROOM-1-N8
- Microcontroller principal cu suport pentru Wi-Fi 6 și Bluetooth 5.
- Comunică prin SPI și I2C cu restul componentelor.
- Dispune de USB nativ (pini IO16 și IO17).

### Afișaj E-Ink 7.5"
- SPI cu semnale CS, DC, RST, BUSY.
- Consumul este aproape zero în modul static.

### Senzor BME688
- Măsoară temperatură, presiune, umiditate și calitatea aerului.
- Comunică prin magistrala I2C.

### Modul RTC DS3231SN
- RTC foarte precis cu suport pentru alimentare backup (supercondensator).
- Conectat tot prin I2C.

### MAX17048
- Fuel gauge pentru monitorizarea stării bateriei.
- Transmite nivelul de încărcare către ESP32 prin I2C.

### MCP73831
- Circuit de încărcare Li-Po cu intrare USB 5V și ieșire controlată.

### SD Card
- Comunicare SPI cu ESP32.
- Folosit pentru stocarea fișierelor e-book.

### Qwiic Connector
- Permite adăugarea rapidă a altor senzori I2C compatibili.

### Butoane
- 3 butoane legate la GPIO-uri.
- Folosite pentru navigarea prin meniu.

---

## 4. Pinii ESP32-C6 folosiți

| Pin ESP32-C6    | Componentă / Semnal         | Funcție                                                                 |
|----------------|------------------------------|--------------------------------------------------------------------------|
| IO7            | MOSI (SPI)                  | Trimitere date SPI                                                        |
| IO2            | MISO (SPI)                  | Citire date SPI                                                           |
| IO6            | CLK (SPI)                   | Clock SPI                                                                 |
| IO10           | CS E-paper                  | Select display                                                            |
| IO5            | DC E-paper                  | Data/Command pentru afișaj                                              |
| IO23           | RST E-paper                 | Reset hardware e-paper                                                    |
| IO3            | BUSY E-paper                | Status e-paper                                                            |
| IO4            | CS SD Card                  | Select card                                                               |
| IO11           | CS Flash extern             | Select memorie                                                            |
| IO22           | I2C SCL                     | Clock pentru I2C                                                          |
| IO21           | I2C SDA                     | Date pentru I2C                                                           |
| IO12, IO13     | USB D-/D+                   | Conexiune USB                                                             |
| IO8            | INT RTC                     | Semnal alarmă de la RTC                                                  |
| IO1            | 32KHz RTC                   | Semnal ceas RTC                                                           |
| IO18           | RESET RTC                   | Reset RTC                                                                 |
| IO9            | Buton BOOT                  | GPIO pentru buton                                                         |
| EN             | Reset                       | Reset general                                                             |
| IO15           | ALERT Fuel Gauge            | Semnal avertizare baterie                                                 |
| GPIO0-19       | Disponibili pentru GPIO-uri | Pot fi folosiți pentru extensii, leduri, debug etc.                     |

---

## 5. Management energetic estimativ

| Componentă                  | Tensiune (V) | Curent estimat (mA) | Observații                                             |
|-----------------------------|--------------|---------------------|----------------------------------------------------------|
| ESP32-C6                   | 3.3          | 80-150              | Depinde de stare (idle, Wi-Fi, BT, etc.)                |
| Display E-paper            | 3.3          | 25 (refresh), 0 (idle) | Doar când actualizează imaginea                      |
| BME688                     | 3.3          | 3.6 max             | Consum redus în standby                               |
| DS3231SN                   | 3.3          | 1                   | RTC constant                                             |
| MAX17048                   | 3.3          | 0.05                | Monitorizare baterie                                     |
| MCP73831                   | 5V           | Depinde de încărcare  | Alimentare baterie Li-Po                                 |
| SD Card                    | 3.3          | 10 max              | Doar când e activ                                        |
| Total estimativ activ      | -            | 120-180             | Variabil în funcție de operație                     |
| Total standby (deep sleep) | -            | sub 0.1             | Autonomie de săptămâni                                 |

---

## 6. Alte informații relevante

- **PCB-ul este cu 2 straturi**, cu plan de masă GND pe top și bottom.
- **Via stitching** aplicat în jurul ESP32 pentru integritate GND.
- Sub antena ESP32 **nu s-au rulat trasee** și PCB-ul a fost decupat conform cerinței.
- Toate **componentele sunt montate pe TOP**.
- Toate **condensatoarele de decuplare** sunt pozițonate cât mai aproape de pinii VCC.

Imagini și randări vor fi adăugate în directorul `Images/`.

---

## 7. Design log

Modelul 3D complet (cu toate componentele, bateria și ecranul) este disponibil în Fusion 360:

**Link Fusion:** *se va insera aici linkul proiectului A360.*

Toate constrângerile au fost respectate conform specificațiilor TSC 2025:
- Plan de masă corect, trasee cu grosimi conforme
- Decupaj sub antenă
- Layer de silkscreen curat
- Test pad-uri marcate
- Gerber și BOM generate corect

---

## [Referințe]
- [Specificații proiect TSC 2025](https://ocw.cs.pub.ro/courses/tsc/proiect2025)
- [Datasheet-uri componente - Mouser / Comet / Waveshare / Bosch / Espressif]
