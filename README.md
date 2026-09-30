# homeassistant-blueprints
Theoretische PV-Leistungsberechnung und Warnung bei Leistungsabfall für Home Assistant.

# Home Assistant Blueprints: Smartes PV-Leistungsmanagement ☀️⚡

Dieses Repository enthält zwei aufeinander abgestimmte Blueprints, um die Leistung deiner Solaranlage (Photovoltaik) in Home Assistant intelligent zu überwachen.

---

## 1. Blueprint: Solarleistung periodisch + bei Strahlungsänderung

Berechnet die theoretisch mögliche PV-Leistung deiner Solarmodule in Watt basierend auf der aktuellen Globalstrahlung (W/m²) deiner Wetterstation. Optional wird der hitzebedingte Leistungsverlust über einen Modultemperatursensor physikalisch exakt miteinbezogen.

### Features
- **Präzise Berechnung:** Nutzt die Wp-Anlagenleistung und die reale Einstrahlung (W/m²).
- **Hitzekorrektur:** Berechnet Temperaturverluste (-0,35%/°C über 25°C).
- **Verlustfaktor:** Berücksichtigt Wechselrichter- und Kabelverluste (z.B. pauschal 10%).
- **Dynamische Trigger:** Berechnet im Zeitraster ODER sofort bei starken Wetterumschwüngen.

---

## 2. Blueprint: Solaranlage: Warnung bei Leistungsabfall

Vergleicht deine echte PV-Erzeugung in Echtzeit mit der theoretisch berechneten Kurve und warnt dich per Smartphone-Benachrichtigung, falls die Leistung einbricht.

### Features
- **Intelligente Verzögerung:** Verhindert Fehlalarme durch vorbeiziehende kleine Wolken.
- **Doppelte Prüfung:** Prüft nach Ablauf der Verzögerung erneut, bevor alarmiert wird.
- **Dämmerungsschutz:** Schaltet sich bei geringer Helligkeit und nachts automatisch ab.

---

## 📋 Einrichtung & Voraussetzungen

### Schritt 1: Nummern-Helfer anlegen
Erstelle unter *Einstellungen -> Geräte & Dienste -> Helfer* einen **Nummer (input_number)** Helfer und benenne ihn `Theoretische PV Leistung Aktuell`.

Damit dieser als echter Leistungssensor mit der Einheit **Watt (W)** vom Energie-Dashboard erkannt wird, füge Folgendes in deine `configuration.yaml` ein:

```yaml
homeassistant:
  customize:
    input_number.theoretische_pv_leistung_aktuell:
      unit_of_measurement: "W"
      device_class: power
      state_class: measurement
      icon: mdi:solar-power
```
*Danach die Home Assistant-Anpassungen über die Entwicklerwerkzeuge neu laden.*

### Tipp bei mehreren Wechselrichtern:
Falls du (wie ich) **zwei Wechselrichter** im Einsatz hast, erstelle vorab einen Helfer vom Typ **"Kombination von Zuständen mehrerer Sensoren"** (Typ: *Summe*). Nutze diese Summen-Entität dann als realen Leistungssensor im Warnungs-Blueprint.

---

## 🚀 Installation

Da dieses Repository öffentlich ist, kannst du die Blueprints über die folgenden Links direkt in deine Home Assistant Instanz importieren. 

*Ersetze beim Klick einfach `DEIN_USERNAME` in der URL mit deinem GitHub-Namen:*

* **Blueprint 1 (Berechnung) importieren:**
  [![Blueprint Importieren](https://home-assistant.io)](https://home-assistant.io)

* **Blueprint 2 (Warnung) importieren:**
  [![Blueprint Importieren](https://home-assistant.io)](https://home-assistant.io)

---

## 📄 Lizenz
Dieses Projekt ist unter der **MIT-Lizenz** lizenziert – siehe die [LICENSE](LICENSE) Datei für Details.

