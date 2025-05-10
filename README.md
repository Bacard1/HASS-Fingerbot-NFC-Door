
![BANNER](/img/banner_HASS-Fingerbot-NFC-Door.png)
# 🖲️ [Zigbee Fingerbot]([figerbot]) CONTROL VIA NFC AND HOME ASSISTANT
[![PayPal Donation](https://img.shields.io/badge/PayPal-Дари-синьо?logo=paypal)](https://www.paypal.com/donate/?hosted_button_id=AAWFZVF2XCP5A)
![Script](https://img.shields.io/badge/logo-yaml-green?logo=yaml)
[![БЪЛГАРСКИ](https://img.shields.io/badge/БЪЛГАРСКИ-език-green?logo=translate&labelColor=gray&style=flat-square&link=https://example.com/en)](BG.md)

> Automate your building entrance with Home Assistant, Zigbee2MQTT and NFC!

This project demonstrates how to control a [Zigbee Fingerbot]([figerbot]) via automation in Home Assistant, triggered by an NFC tag placed near the building's main entrance. When the tag is scanned (e.g., with a smartphone), the Fingerbot activates and presses a physical button — such as one for the intercom or door unlocking.

🔧 Technologies used<br>
🏠 Home Assistant<br>
📶 Zigbee2MQTT<br>
🤖 [Zigbee Fingerbot]([figerbot])<br>
📱 NFC tag (compatible with Android/iOS)<br>
⚙️ MQTT automations

✅ Use Cases  
Unlock the main entrance by scanning<br>
Simulate a button press with a robotic arm<br>
Contactless access without physical keys

🚀 Benefits  
Fully local and offline operation<br>
Fast NFC scan response (around 1 second)<br>
Easily customizable YAML code<br>
Option to add notifications or logs

---

## 📦 CONTENT

- [🖲️ [Zigbee Fingerbot]([figerbot]) CONTROL VIA NFC AND HOME ASSISTANT](#️-zigbee-fingerbot-control-via-nfc-and-home-assistant)
	- [📦 CONTENT](#-content)
	- [💥 IDEA](#-idea)
	- [⚙️ [Zigbee Fingerbot]([figerbot]) TUYA TS0001: a good choice with all necessary options, built-in battery and Type-C charging:](#️-zigbee-fingerbot-tuya-ts0001-a-good-choice-with-all-necessary-options-built-in-battery-and-type-c-charging)
	- [💫 NFC](#-nfc)
		- [INSTALLING NFC IN HOME ASSISTANT:](#installing-nfc-in-home-assistant)

---

## 💥 IDEA  
Electric entrance locks in most apartment buildings are not powered with high voltage, but rather low voltage used as a signal to the electric lock to detect that someone is pressing the button from their apartment. In reality, the button just connects the wires together. I decided to **buy** a [[Zigbee Fingerbot]([figerbot])](figerbot) to press this button and the problem was solved… well, not quite! The **springs** used in these buttons to keep them in the "off" state are quite **stiff**, and the [[Zigbee Fingerbot]([figerbot])](figerbot) couldn’t handle it.  
<br>

Then I realized that if the [[Zigbee Fingerbot]([figerbot])](figerbot) can’t press the switch, it could instead **connect the wires directly**, just like the button does. And since no live voltage flows through those wires, **an electrician isn’t needed** — I could do it myself.<br>

> [!CAUTION]  
> Always check the wires with a multimeter for voltage!

> I created a sample diagram to help visualize the intended result:

![shema](/img/shema_HASS-Fingerbot-HFC-Door.png)

| After removing the switch, I used [wire connectors](klamma) to pull out both wires next to the switch. This way, the switch remains functional and the [[Zigbee Fingerbot]([figerbot])](figerbot) can do its job. | ![klamma](/img/klamma.png)  |
|-----|-----|

## ⚙️ [[Zigbee Fingerbot]([figerbot]) TUYA TS0001:](figerbot) a good choice with all necessary options, built-in battery and Type-C charging:

|![Fingerbot](/img/Fingerbot.png)|![Fingerbot option](/img/Fingerbot_option.png)|
|-----|-----|

| **Option** | **Description** |
|-----------|-----------------|
| **State** | `ON`/`OFF` state — triggers or deactivates button press. |
| **Battery** | Remaining battery percentage. Can take up to 24 hours to update. |
| **Mode** | Operating mode:<br>• `Click` – short press<br>• `Switch` – toggle on/off<br>• `Program` – custom behavior (depends on firmware). |
| **Lower** | Down movement limit – how far the arm moves down (in %). |
| **Upper** | Up movement limit – how far the arm retracts (in %). |
| **Delay** | How long the arm holds the button (in seconds). |
| **Reverse** | Reverses motor direction (useful when mounted upside down). |
| **Touch** | Enables or disables manual touch activation. |
| **Linkquality** | Signal strength (`LQI`) — higher is better. |

> Photos of the installed [[Zigbee Fingerbot]([figerbot])](figerbot)

|![img](/img/photo001.jpg)|![img](/img/photo002.jpg)|
|----|----|
|![img](/img/photo003.jpg)|![img](/img/phofo004.jpg)|

## 💫 NFC  
The most popular NFC tags compatible with nearly all devices are [ntag213](NFCtag1) and [ntag215](NFCtag2). I recommend [ntag213](NFCtag1) — it works best with my phone and the rest of my family’s devices.

> [!TIP]  
> When choosing an NFC tag, make sure it is **rewritable**!

### INSTALLING NFC IN HOME ASSISTANT:  
NFC tags are configured via a mobile device and the Home Assistant app. My device is [POCO X3 NFC PRO](poco) running [HyperOS 2](hyperos).

| From the menu, go to Settings. | Choose App Configuration. |
|----|----|
| ![nfc](/img/nfc/nfctag1.png) | ![nfc](/img/nfc/nfctag2.png) |

| Go to NFC Tags. | After scanning, choose Create Event. |
|----|----|
| ![nfc](/img/nfc/nfctag3.png) | ![nfc](/img/nfc/nfctag4.png) |

| In HASS main menu, go to Tags. | You will see the new tag by the scanned ID. |
|----|----|
| ![nfc](/img/nfc/nfctag5.png) | ![nfc](/img/nfc/nfctag6.png) |

| Tap the 3 dots of the new tag and select “New Automation”. | Add [[Zigbee Fingerbot]([figerbot])](figerbot) as the action. |
|----|----|
| ![nfc](/img/nfc/nfctag7.png) | ![nfc](/img/nfc/nfctag8.png) |

> AUTOMATION YAML CODE:
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
	  message: Home Assistant Unlock the front door!
mode: single
```

> [!TIP]  
> If you enjoyed this project, you can find more interesting repositories [HERE](https://github.com/Bacard1?tab=repositories).  
> If you need help or have any questions, feel free to contact me.

[hyperos]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
[poco]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
[klamma]: https://de.aliexpress.com/item/1005005805414976.html?spm=a2g0o.order_list.order_list_main.212.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[figerbot]: https://de.aliexpress.com/item/1005008341830865.html?spm=a2g0o.order_list.order_list_main.363.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag1]: https://de.aliexpress.com/item/1005007613908773.html?spm=a2g0o.order_list.order_list_main.394.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag2]: https://de.aliexpress.com/item/1005006332360160.html?spm=a2g0o.order_list.order_list_main.217.21c85c5f8qzzfj&gatewayAdapt=glo2deu
