# Proiect TSC 2025 – OpenBook

## 🔧 Descriere generală

OpenBook este un dispozitiv portabil de tip e-book reader bazat pe ESP32-C6. Proiectul a fost realizat în cadrul cursului Tehnici de Sistem pe Cip (TSC) de la Facultatea de Automatică și Calculatoare – UPB. Dispozitivul conține un ecran e-paper, butoane de control, senzor de mediu, ceas de timp real și posibilitate de alimentare de la baterie Li-Po, fiind gândit ca un sistem eficient energetic și scalabil.

---

## 📊 1. Diagramă bloc

![Diagramă bloc](https://docs.google.com/drawings/d/1UpxRyJNfczJHhNRvWdeb5kh_7IEUy5173odk93W_GSA/export/png)

---

## 🧾 2. Bill of Materials (BOM)

| Componentă | Cod | Magazin | Datasheet |
|-----------|------|---------|-----------|
| ESP32-C6-WROOM-1-N8 | U2 | [Mouser](https://www.mouser.com/ProductDetail/Espressif/ESP32-C6-WROOM-1-N8) | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_datasheet_en.pdf) |
| Ecran e-paper 7.5" | WSH-13187 | [Waveshare](https://www.waveshare.com/7.5inch-e-paper-hat.htm) | [Datasheet](https://files.waveshare.com/upload/6/60/7.5inch_e-Paper_V2_Specification.pdf) |
| Baterie LiPo 2500mAh | LPS84174 | [Comet](https://www.comet-electronique.com) | [Datasheet](https://cdn.sparkfun.com/assets/c/4/5/a/e/LPS84174.pdf) |
| MCP73831 (Battery Charger) | U5 | [Mouser](https://www.mouser.com/ProductDetail/Microchip/MCP73831T-2ACI-OT) | [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/20001984g.pdf) |
| MAX17048 (Fuel Gauge) | U4 | [Mouser](https://www.mouser.com/ProductDetail/Maxim-Integrated/MAX17048G%2BT10) | [Datasheet](https://datasheets.maximintegrated.com/en/ds/MAX17048.pdf) |
| DS3231 (RTC) | U3 | [Mouser](https://www.mouser.com/ProductDetail/Maxim-Integrated/DS3231SN) | [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS3231.pdf) |
| BME688 | SENSOR2 | [Mouser](https://www.mouser.com/ProductDetail/Bosch-Sensortec/BME688) | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme688-ds001.pdf) |
| Butoane tactile 3x | EVQ-PUJ02K | [Mouser](https://www.mouser.com/ProductDetail/Panasonic/EVQ-PUJ02K) | [Datasheet](https://na.industrial.panasonic.com/sites/default/pidsa/files/evqpu.pdf) |
| SD Card Socket | 112A-TAAR-R03 | [Comet](https://store.comet.srl.ro/Catalogue/Product/43497/) | [Datasheet](https://www.hirose.com/en/product/document?clcode=CL0581-0013-0-00&productname=112A-TAAR&series=112A&documenttype=Catalog&lang=en&documentid=D109234_en) |

> Alte componente pasive (rezistențe, condensatori) sunt în capsulă 0402 și nu sunt incluse individual în tabel.

---

## ⚙️ 3. Funcționalitate hardware detaliată

### ESP32-C6-WROOM-1

- Microcontroller principal, cu conectivitate WiFi 6 și USB 2.0.
- Are suport pentru SPI și I2C, ideale pentru conectarea senzorilor și afișajului.
- Rulează codul care gestionează meniul, ecranul, senzorii și datele de pe SD Card.

### Ecran e-paper 7.5" Waveshare

- Conectat prin SPI (CLK, MOSI, CS, DC, RST, BUSY).
- Rezoluție 800x480, consum zero în static.
- Ideal pentru afișaj de tip e-book.

### Alimentare și management baterie

- Baterie LiPo de 2500mAh, încărcată prin MCP73831.
- Fuel gauge MAX17048 pentru monitorizarea tensiunii și nivelului de încărcare.
- LDO separat pentru 3.3V (ex. XC6220).

### RTC – DS3231

- Timp real precis, backup cu supercap.
- Conectat prin I2C.

### Senzor BME688

- Măsoară temperatură, presiune, umiditate, calitate aerului.
- Legat pe magistrala I2C comună.

### SD Card

- Slot conectat prin SPI pentru stocarea cărților în format .txt.

### Butoane

- 3 butoane pentru navigare.
- Fiecare legat la câte un GPIO (cu rezistențe de pull-down).

---

## 🔌 4. Pinout ESP32-C6 și justificări

| Pin ESP32-C6 | Funcție | Componentă | Motiv |
|--------------|--------|------------|-------|
| GPIO1        | SDA    | BME688, MAX17048, DS3231 | I2C |
| GPIO2        | SCL    | BME688, MAX17048, DS3231 | I2C |
| GPIO3        | CS     | E-Paper    | SPI control |
| GPIO4        | RST    | E-Paper    | Reset hardware |
| GPIO5        | DC     | E-Paper    | Control semnal date/comenzi |
| GPIO6        | CLK    | E-Paper    | SPI clock |
| GPIO7        | MOSI   | E-Paper    | SPI date |
| GPIO8        | BUSY   | E-Paper    | Status afișaj |
| GPIO9        | BTN1   | Buton #1   | Navigare pagină |
| GPIO10       | BTN2   | Buton #2   | Înapoi |
| GPIO11       | BTN3   | Buton #3   | Confirmare |
| GPIO12       | CS     | SD Card    | Chip Select SPI |
| GPIO13       | CLK    | SD Card    | SPI clock |
| GPIO14       | MISO   | SD Card    | SPI dată IN |
| GPIO15       | MOSI   | SD Card    | SPI dată OUT |

---

## 🔋 Estimare consum

| Modul | Consum (tipic) |
|-------|----------------|
| ESP32-C6 | 80mA activ, 10µA deep sleep |
| E-Paper | 25mA în refresh |
| BME688 | 3.6mA activ, 2µA standby |
| DS3231 | 3mA activ |
| MAX17048 | <100µA |
| MCP73831 | până la 1A (la încărcare) |

---

## 📐 Alte informații utile

- Design-ul 3D a fost realizat în Fusion360, iar fișierul .step este inclus în folderul `Mechanical`.
- Decupajul sub antena ESP32 a fost realizat conform specificațiilor.
- Condensatorii de decuplare de 100nF sunt poziționați aproape de pinii de alimentare.
- Nu s-au folosit unghiuri drepte în rutare.
- Componentele sunt toate SMD pe layer-ul TOP.

---

## 🖼️ Randări și imagini

Imagini cu asamblarea dispozitivului, randări 3D și capturi din Fusion360 pot fi găsite în folderul `Images`.

---

## 📎 Design log și surse

- [Design log Fusion360](https://a360.co/4kX1RTV)
- [Fișiere Gerber și BOM](./Manufacturing/)
- [Documentația oficială a proiectului TSC](https://ocw.cs.pub.ro/courses/tsc/proiect2025)

---

