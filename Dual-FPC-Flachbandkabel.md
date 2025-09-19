Die LCD-Digitizer-Einheit der Samsung Galaxy A-Serie (A01 bis A04e) verwendet typischerweise ein **kombiniertes Dual-FPC-Flachbandkabel**, das sowohl das **Display** als auch den **Touch-Digitizer** versorgt. Hier sind die wichtigsten technischen Details und Hinweise zur Pinstruktur und Signalführung:

---

## 📦 Aufbau des Dual-FPC-Kabels

Die Einheit besteht aus zwei nebeneinanderliegenden Flachbandkabeln, die in einem gemeinsamen Stecker oder flexiblen Träger zusammengeführt sind:

### 1. **Display-FPC (LCD-Ansteuerung)**
- **Signaltyp:** MIPI DSI (Display Serial Interface)
- **Spannung:** meist 1.8 V oder 2.8 V
- **Pins:** typischerweise 20–40 Pins
- **Funktionen:**
  - DSI Data Lanes (D0+, D0−, D1+, D1− …)
  - DSI Clock (CLK+, CLK−)
  - Backlight Enable / PWM
  - Power (VDD, VDDIO)
  - Ground

### 2. **Touch-Digitizer-FPC**
- **Signaltyp:** I²C oder SPI (abhängig vom Controller)
- **Spannung:** meist 1.8 V oder 3.3 V
- **Pins:** typischerweise 6–10 Pins
- **Funktionen:**
  - I²C SDA/SCL
  - Interrupt (INT)
  - Reset
  - Power (VDD)
  - Ground

---

## 🔍 Display-Controller und Touch-ICs

Die Samsung A-Serie verwendet häufig folgende Komponenten:

| Modell | Display-IC | Touch-IC | Bemerkung |
|--------|------------|----------|-----------|
| A01    | Himax HX8369 | GT911 oder FT5x06 | 720×1520 LCD |
| A02    | Novatek NT35510 | GT911 | 720×1600 LCD |
| A03/A04 | Ilitek ILI9881C | GT911 oder Goodix | 720×1600 LCD |

Diese ICs sind **nicht dokumentiert für Bastlerzwecke**, aber es gibt Reverse-Engineering-Projekte, z. B. bei [LCDWiki](http://www.lcdwiki.com/) oder [Panelook](https://www.panelook.com/).

---

## 🧪 Experimentelle Nutzung mit Raspberry Pi

Wenn du das Dual-FPC-Kabel auf **Dupont-Header** herausführen willst, brauchst du:

- **FPC-Adapterplatine** mit 0.5 mm oder 1.0 mm Pitch
- **Level-Shifter** für 1.8 V ↔ 3.3 V
- **MIPI DSI zu HDMI Bridge** (z. B. TC358779XBG) oder FPGA
- **Touch-Controller-Adapter** (z. B. I²C zu USB oder direkt an Pi GPIO)

⚠️ **Wichtig:** MIPI DSI ist **nicht direkt über GPIO oder Dupont-Kabel nutzbar** – du brauchst eine Bridge oder native DSI-Unterstützung (wie beim Raspberry Pi DSI-Port).

---

## 🧭 Nächste Schritte

Wenn du mir sagst, welches Display du konkret hast (z. B. Modellnummer auf dem Flexkabel), kann ich dir helfen:

- Das Pinout zu rekonstruieren
- Einen Adapterplan zu entwerfen
- Touch-IC über I²C am Pi zu betreiben

Willst du das Display nur als Anzeige nutzen oder auch den Touchscreen einbinden?
