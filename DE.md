![BANNER](/img/banner_HASS-Fingerbot-NFC-Door.png)
# 🖲️ STEUERUNG VON ZIGBEE [FINGERBOT] ÜBER NFC UND HOME ASSISTANT
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?color=ff00d8)](https://opensource.org/licenses/MIT)
![GitHub last commit](https://img.shields.io/github/last-commit/Bacard1/HASS-Fingerbot-NFC-Door.svg?color=ff00d8)
[![hacs_badge](https://img.shields.io/badge/HACS-2025.5.3-orange.svg?color=ff00d8)](https://github.com/hacs/integration)

[![Home Assistant](https://img.shields.io/badge/.-HOME_ASSISTANT-blue?logo=homeassistant)](https://www.home-assistant.io/) 
[![Donate via PayPal](https://img.shields.io/badge/PayPal-DONATE-blue?logo=paypal)](https://www.paypal.com/donate/?hosted_button_id=AAWFZVF2XCP5A)
![Script](https://img.shields.io/badge/Script-YAML-blue?logo=yaml)

[![Български](https://img.shields.io/badge/BG-ЕЗИК-gree?logo=translate&labelColor=gray&style=flat-square&link=https://example.com/bg
)](BG.md)
[![Deutch](https://img.shields.io/badge/DE-SPRACHE-gree?logo=translate&labelColor=gray&style=flat-square&link=https://example.com/bg
)](DE.md)
[![English](https://img.shields.io/badge/EN-LANGUAGE-gree?logo=translate&labelColor=gray&style=flat-square&link=https://example.com/bg)](README.md)

> Automatisieren Sie den Gebäudezugang mit Home Assistant, Zigbee2MQTT und NFC!

Dieses Projekt zeigt, wie Sie einen Zigbee Fingerbot über eine Automatisierung in Home Assistant steuern können, die durch einen NFC-Tag ausgelöst wird, der neben der Gebäudeeingangstür angebracht ist. Beim Scannen des Tags (z. B. mit einem Smartphone) wird der Fingerbot aktiviert und drückt physisch einen Knopf – beispielsweise den für die Gegensprechanlage oder die Türöffnung.

🔧 Verwendete Technologien<br>
🏠 Home Assistant<br>
📶 Zigbee2MQTT<br>
🤖 Zigbee Fingerbot<br>
📱 NFC-Tag (kompatibel mit Android/iOS)<br>
⚙️ MQTT-Automatisierungen

✅ Anwendungen
Entsperren der Eingangstür durch Scannen<br>
Simulieren eines Knopfdrucks mit einem Roboterarm<br>
Berührungsloser Zugang zum Gebäude ohne physischen Schlüssel<br>

🚀 Vorteile
Vollständig lokale und offline Funktionsweise<br>
Schnelle Reaktion auf NFC-Scan (ca. 1 Sekunde)<br>
Einfach anpassbarer YAML-Code<br>
Möglichkeit, Benachrichtigungen oder Protokolle hinzuzufügen

---

## 📦 INHALT

- [🖲️ STEUERUNG VON ZIGBEE \[FINGERBOT\] ÜBER NFC UND HOME ASSISTANT](#️-steuerung-von-zigbee-fingerbot-über-nfc-und-home-assistant)
  - [📦 INHALT](#-inhalt)
  - [💥 IDEE](#-idee)
  - [⚙️ Zigbee Fingerbot TUYA TS0001: ist eine gute Wahl mit allen notwendigen Optionen für dieses Gerät und eingebautem Akku sowie Typ-C-Ladeanschluss:](#️-zigbee-fingerbot-tuya-ts0001-ist-eine-gute-wahl-mit-allen-notwendigen-optionen-für-dieses-gerät-und-eingebautem-akku-sowie-typ-c-ladeanschluss)
  - [💫 NFC](#-nfc)
    - [INSTALLATION VON NFC IN HOME ASSISTANT:](#installation-von-nfc-in-home-assistant)

---

## 💥 IDEE  
Die elektrischen Türschlösser der meisten städtischen **Gebäude** werden nicht mit **Hochspannung** betrieben, sondern mit Niederspannung, die als Signal an das elektrische Schloss dient, um zu erkennen, dass jemand den Knopf in seiner Wohnung drückt. Tatsächlich verbindet der Knopf einfach die Kabel miteinander. Ich beschloss, einen [Zigbee Fingerbot][figerbot] zu kaufen, der diesen Knopf drücken sollte, und das Problem war gelöst... ja, aber nein! Die **Federn**, die an diesen Schaltern angebracht sind, um sie immer im ausgeschalteten Zustand zu halten, wenn sie nicht gedrückt werden, sind ziemlich **hart**, und der [Zigbee Fingerbot][figerbot] konnte sie nicht bewältigen!  
<br>  

Ich dachte mir, dass, wenn der [Zigbee Fingerbot][figerbot] den Schalter nicht drücken kann, **er die Kabel miteinander verbinden könnte**, genau wie es Ihr Knopf tut, und da durch die Kabel kein Strom fließt, **wäre kein Elektriker notwendig**, und ich könnte es selbst machen.<br>

> [!CAUTION]  
> Überprüfen Sie dennoch immer die Kabel mit einem Multimeter auf Spannung!

> Ich habe ein Beispielschema erstellt, damit Sie sich das Ergebnis vorstellen können:

![shema](/img/shema_HASS-Fingerbot-HFC-Door.png)

| Nach dem Demontieren des Schalters verwendete ich solche [Kabelverbinder][klamma], um beide Kabel seitlich vom Schalter herauszuführen. So bleibt der Schalter funktionsfähig, und der [Zigbee Fingerbot][figerbot] kann arbeiten. | ![klamma](/img/klamma.png)  |
|-----|-----|

## ⚙️ [Zigbee Fingerbot TUYA TS0001:]([[figerbot]]) ist eine gute Wahl mit allen notwendigen Optionen für dieses Gerät und eingebautem Akku sowie Typ-C-Ladeanschluss:

|![Fingerbot](/img/Fingerbot.png)|![Fingerbot option](/img/Fingerbot_option.png)|
|-----|-----|


| **Option** | **Beschreibung** |
| ----- | ---- |
| **State** | Zustand `ON`/`OFF` – aktiviert oder deaktiviert das Drücken des Knopfs.|
| **Battery** | Verbleibender Akkuladestand in Prozent (`%`). Die Aktualisierung kann bis zu 24 Stunden dauern. |
| **Mode** | Betriebsmodus – bestimmt das Verhalten des Fingerbots:<br>• `Click` – Kurzes Drücken<br>• `Switch` – Umschalten zwischen gedrückt und losgelassen<br>• `Program` – Benutzerdefiniertes Verhalten (abhängig vom Firmware). |
| **Lower** | **Untere Bewegungsgrenze** – legt fest, wie weit sich der Arm nach unten bewegt (in %). |
| **Upper** | **Obere Bewegungsgrenze** – legt fest, wie weit sich der Arm nach dem Drücken zurückzieht (in %). |
| **Delay** | **Haltezeit** – wie lange der Arm den Knopf gedrückt hält (in Sekunden). |
| **Reverse** | Wenn aktiviert, **kehrt es die Bewegungsrichtung des Motors um** (nützlich bei umgekehrter Installation). |
| **Touch** | Aktiviert oder deaktiviert die **manuelle Aktivierung durch Berühren** des Geräts. |
| **Linkquality** | Signalqualität (`LQI`) – ein höherer Wert bedeutet eine bessere Zigbee-Verbindung.|

> Fotos des bereits installierten [Zigbee Fingerbot][figerbot]

> 
|![img](/img/photo001.jpg)|![img](/img/photo002.jpg)|![img](/img/photo003.jpg)|![img](/img/phofo004.jpg)|
|----|----|----|----|


## 💫 NFC  
Die beliebtesten NFC-Tags, die mit fast allen Geräten kompatibel sind, sind [ntag213][NFCtag1] und [ntag215][NFCtag2]. Ich empfehle [ntag213][NFCtag1] – mein Telefon funktioniert besser damit, ebenso wie die Geräte der anderen Familienmitglieder.

> [!TIP]  
> Stellen Sie beim Kauf von NFC-Tags sicher, dass sie **beschreibbar** sind!

### INSTALLATION VON NFC IN HOME ASSISTANT:  
NFC-Tags werden über ein mobiles Gerät und die Home Assistant App eingerichtet. Mein Gerät ist ein [POCO X3 NFC PRO][poco] mit installiertem [HyperOS 2][hyperos].

| Wählen Sie im Menü „Einstellungen“. | Wählen Sie „App-Optionen“. |
|----|----|
| ![nfc](/img/nfc/nfctag1.png) | ![nfc](/img/nfc/nfctag2.png) |

| Gehen Sie zu „NFC-Tags“. | Nach dem Scannen des Tags wählen Sie „Ereignis erstellen“. |
|----|----|
| ![nfc](/img/nfc/nfctag3.png) | ![nfc](/img/nfc/nfctag4.png) |

| Öffnen Sie im Home Assistant-Hauptmenü „Tags“. | Dort sehen Sie den neuen Tag. Sie erkennen ihn an der ID,<br> die beim Scannen angezeigt wurde. |
|----|----|
| ![nfc](/img/nfc/nfctag5.png) | ![nfc](/img/nfc/nfctag6.png) |

| Wählen Sie die drei Punkte oben rechts beim neuen Tag und <br> wählen Sie „Neue Automatisierung“. | Fügen Sie den [Zigbee Fingerbot][figerbot] zu den Aktionen hinzu. |
|----|----|
| ![nfc](/img/nfc/nfctag7.png) | ![nfc](/img/nfc/nfctag8.png) |

> AUTOMATISIERUNGSCODE:
```yaml
alias: Tag tag opening door b2a06299-1e6a-4ae1-8d6c-ac50d26f3d67 has been scanned
description: ""
triggers:
  - trigger: tag
    tag_id: 8b3a2946-73d2-4f74-9933-b7299f2abfa1
conditions: []
actions:
  - action: switch.turn_on
    metadata: {}
    data: {}
    target:
      entity_id: switch.fingerrobot_001
  - action: notify.user
    metadata: {}
    data:
      title: Home Assistant Information!
      message: Home Assistant hat die Haustür entriegelt!
mode: single
```

> [!TIP]
> Wenn Ihnen dieses Projekt gefallen hat, finden Sie [HIER](https://github.com/Bacard1?tab=repositories) weitere interessante Repositories von mir.<br>
> Wenn Sie Schwierigkeiten haben oder Fragen haben, zögern Sie nicht, mich zu kontaktieren.

[hyperos]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
[poco]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
[klamma]: https://de.aliexpress.com/item/1005005805414976.html?spm=a2g0o.order_list.order_list_main.212.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[figerbot]: https://de.aliexpress.com/item/1005008341830865.html?spm=a2g0o.order_list.order_list_main.363.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag1]: https://de.aliexpress.com/item/1005007613908773.html?spm=a2g0o.order_list.order_list_main.394.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag2]: https://de.aliexpress.com/item/1005006332360160.html?spm=a2g0o.order_list.order_list_main.217.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[hyperos]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
