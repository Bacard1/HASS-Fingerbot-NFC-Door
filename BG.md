![BANNER](/img/banner_HASS-Fingerbot-NFC-Door.png)
# 🖲️ УПРАВЛЕНИЕ НА ZIGBEE FIGERBOT ЧРЕЗ NFC И HOME ASSISTANT
[![PayPal дарение](https://img.shields.io/badge/PayPal-Дари-синьо?logo=paypal)](https://www.paypal.com/donate/?hosted_button_id=AAWFZVF2XCP5A)
![Скрипт](https://img.shields.io/badge/logo-yaml-green?logo=yaml)
[![English](https://img.shields.io/badge/ENGLICH-language-green?logo=translate&labelColor=gray&style=flat-square&link=https://example.com/en)](README.md)

> Автоматизирай входа на сградата с Home Assistant, Zigbee2MQTT и NFC!

Този проект показва как да управляваш Zigbee Fingerbot чрез автоматизация в Home Assistant, задействана от NFC таг, поставен до входната врата на сградата. При сканиране на тага (напр. със смартфон), Fingerbot се активира и натиска физически бутон — например този за домофон или отключване.

🔧 Използвани технологии<br>
🏠 Home Assistant<br>
📶 Zigbee2MQTT<br>
🤖 Zigbee Fingerbot<br>
📱 NFC таг (съвместим с Android/iOS)<br>
⚙️ MQTT автоматизации

✅ Приложения
Отключване на входна врата чрез сканиране<br>
Симулиране на натискане на бутон с роботизирана ръка<br>
Безконтактен достъп до сграда без физически ключ<br>

🚀 Предимства
Напълно локална и офлайн работа<br>
Бърза реакция при NFC сканиране (около 1 секунда)<br>
Лесно персонализируем YAML код<br>
Възможност за добавяне на известия или логове

---

## 📦 СЪДЪРЖАНИЕ

- [🖲️ УПРАВЛЕНИЕ НА ZIGBEE FIGERBOT ЧРЕЗ NFC И HOME ASSISTANT](#️-управление-на-zigbee-figerbot-чрез-nfc-и-home-assistant)
	- [📦 СЪДЪРЖАНИЕ](#-съдържание)
	- [💥 ИДЕЯ](#-идея)
	- [🛠️ ПОДГОТОВКА](#️-подготовка)

---

## 💥 ИДЕЯ
Електрическите входни брави на повечето градски згради не се оправляват с високо напрежение, а напротив с ниско напрежение което служи за сигнал на електрическата брава за да разбере че някои натиска бутонът в домът си. Всъщност той просто допира кабелите един в друг. Реших да захупя [Zigbee Fingerbot]([figerbot]) който да натиска този бутон и проблемът беше решен, да ама не! Прожините който се слагат на тези ключове за да са винаги в изглючено състояние без натиск са доста корави и [Zigbee Fingerbot]([figerbot]) не успя да се справи!
<br>

Замислих се че след като [Zigbee Fingerbot]([figerbot]) не може да натисне ключът той ще допира кабелите един в друг, точно така както прави и ключът Ви, а по кабелите не тече ток, така че няма да е необходим ел. техник и ще се справя и сам.<br>

> [!CAUTION]
> Въпреки това винаги проверявайте кабелите с мултицет за напрежение!

> Изработих примерна схема за ди си представите какъв трябва да е резултатът:

![shema](/img/shema_HASS-Fingerbot-HFC-Door.png)



## 🛠️ ПОДГОТОВКА



> [!TIP]
> Ако този проект ви е харесъл, [ТУК](https://github.com/Bacard1?tab=repositories) ще намерите още интересни гранилища направени от мен.<br>
> Ако срещате затруднения или имате въпроси не се колебайте да се свържете с мен.

[figerbot]: https://de.aliexpress.com/item/1005008341830865.html?spm=a2g0o.order_list.order_list_main.363.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag1]: https://de.aliexpress.com/item/1005007613908773.html?spm=a2g0o.order_list.order_list_main.394.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag2]: https://de.aliexpress.com/item/1005006332360160.html?spm=a2g0o.order_list.order_list_main.217.21c85c5f8qzzfj&gatewayAdapt=glo2deu