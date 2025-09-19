# Ich möchte ein **einheitliches Display-Modul** verwenden, das mit den folgenden Samsung-Modellen kompatibel ist:

- **Samsung Galaxy A01**
- **Samsung Galaxy A02**
- **Samsung Galaxy A03**
- **Samsung Galaxy A04**
- **Samsung Galaxy A04s**
- **Samsung Galaxy A04e**

---

## 📱 Display-Kompatibilität dieser Modelle

Die genannten Geräte teilen sich eine sehr ähnliche Display-Spezifikation:

- **Größe:** 6.5 Zoll
- **Typ:** PLS LCD
- **Auflösung:** 720 × 1600 Pixel (HD+)
- **Seitenverhältnis:** 20:9
- **Touch:** Kapazitiv, meist mit Goodix GT911 oder ähnlichem I²C-Controller
- **Interface:** MIPI DSI für das Display, I²C für den Touch-Digitizer
- **Backlight:** PWM oder Enable-Pin, meist 3.3 V oder 5 V

Die **mechanische Bauform und das Flexkabel-Layout** sind bei den A02 bis A04e sehr ähnlich. Viele Ersatzteilhändler verkaufen ein und dasselbe LCD-Digitizer-Modul als kompatibel mit **mehreren dieser Modelle**.

🔧 Beispiel: Ein Ersatzdisplay mit der Bezeichnung „**GH82-XXXXXA**“ kann für A02, A03 und A04 verwendet werden – oft mit identischem 40-Pin-FPC-Stecker.

---

## 🧠 Was du brauchst für dein HAT-Projekt

Um ein universelles HAT zu bauen, das dieses Display unterstützt, brauchst du:

### 1. **FPC-Connector für das Display**
- 40-Pin oder 50-Pin FPC mit 0.5 mm Pitch
- Breakout auf 2.54 mm Dupont-Header
- Optional: Flip-Lock oder ZIF-Connector

### 2. **Signalgruppen auftrennen**
- **MIPI DSI:** Nicht direkt über GPIO nutzbar – nur über native DSI-Port oder Bridge (z. B. TC358779XBG)
- **Touch-Digitizer:** I²C → direkt an Raspberry Pi GPIO anschließbar
- **Backlight:** PWM oder Enable → steuerbar über GPIO oder MOSFET

### 3. **Spannungsversorgung**
- 1.8 V für DSI-Signale
- 3.3 V für Touch-Controller
- 5 V für Backlight (je nach Modell)

### 4. **Optional: EEPROM oder DIP-Schalter**
- Für Display-Identifikation oder manuelle Konfiguration

---

## 🧪 Vorschlag für dein HAT-Design

| Modulbereich | Funktion | Anschluss |
|--------------|----------|-----------|
| FPC-Connector | Display + Touch | 40–50 Pins |
| Dupont-Header | Experimentelle Signale | 2.54 mm |
| Level-Shifter | 1.8 V ↔ 3.3 V | TXS0108E o. ä. |
| Touch-I²C | SDA/SCL/INT/RESET | GPIO 2/3/4/17 |
| Backlight-Treiber | PWM oder Enable | GPIO + MOSFET |
| DSI-Bridge (optional) | MIPI DSI → HDMI | TC358779XBG oder FPGA |

---
