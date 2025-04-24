# ⚡ Dynamische Strompreissteuerung Zendure V2.0

Dieses Home Assistant Blueprint/Script automatisiert die Steuerung eines Zendure Batteriespeichersystems basierend auf aktuellen Strompreisen, PV-Leistung und Batterieladung.

## 🌍 Funktion

Das Skript trifft Entscheidungen, wann und wie der Zendure-Batteriespeicher betrieben werden soll:

⚡ Funktion der Automatisierung:

 - Grundlastentladung (0 - 8 Uhr): In den frühen Morgenstunden wird die Batterie verwendet, um die Grundlast des Haushalts zu decken. Die Batterie wird mit einer Leistung von 120 W entladen, um diese Grundlast zu versorgen.

 - PV-Überschussnutzung am Nachmittag (16 - 18 Uhr): Wenn genügend Solarstrom erzeugt wird und die Batterie eine hohe Ladung (> 80 %) hat, wird das Ziel sein, den Akku bis zum Ende des Tages voll aufzuladen, um zu vermeiden, dass der Bypass-Modus aktiviert wird und Solarstrom vergeudet wird. Es geht also nicht um das Entladen der Batterie, sondern um die Optimierung der Speicherung.

 - Teure Zeiten (Smart-Modus): Bei hohen Strompreisen wird der Zendure-Batteriespeicher in den Smart-Modus geschaltet. In diesem Modus wird versucht, eine 0 Einspeisung zu realisieren, indem der Haushalt vollständig aus der Batterie versorgt wird, um teuren Strom aus dem Netz zu vermeiden.

 - Extrem günstige Zeiten (unter dem Minimum): Wenn der Strompreis sehr niedrig ist, wird Netzstrom verbraucht, da dieser günstig ist. Gleichzeitig wird überschüssiger Solarstrom in der Batterie gespeichert, um diesen für teurere Zeiten zu nutzen.

 - Leicht unter Durchschnitt, tagsüber: Wenn der Strompreis unter dem Durchschnitt liegt, wird während des Tages die Grundlast des Haushalts aus der Batterie gedeckt (mit einer Leistung von 120 W). Hierbei wird die Batterie leicht entladen, um die laufenden Haushaltskosten zu decken.

🔋 Laden der Batterie:

 - „Aus“-Modus: Wenn der Zendure-Batteriespeicher ausgeschaltet ist, wird die Batterie durch die PV-Anlage (Photovoltaikanlage) aufgeladen, um überschüssigen Solarstrom zu speichern und die Batterie für spätere Zeiten vorzubereiten.

## ⚙ Voraussetzungen

 - HACS: https://www.hacs.xyz/
 - Tibber Integration: https://www.home-assistant.io/integrations/tibber/
 - Zendur Integration: https://github.com/fireson/zendure-ha

- Sensoren:
  - `sensor.dynamischer_strompreis`: Liefert aktuelle Strompreise. (Tibber)
  - `sensor.pv_leistung`: Aktuelle PV-Erzeugung. (Zendure)
  - `sensor.batteriestand`: Aktueller Ladezustand der Batterie. (Zenture)
- Zendure-Komponenten:
  - `select.zendure_manager_operation` (Zenture)
  - `number.zendure_manager_manual_power` (Zenture)

## ⏱ Trigger

- Stündlich (jede volle Stunde)
- Bei Änderungen der Strompreise oder PV-Leistung
