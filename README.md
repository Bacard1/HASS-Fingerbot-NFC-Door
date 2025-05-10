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
	- [⚙️ Zigbee Fingerbot TUYA TS0001: е добър избор със всички опции необходими за това устройство и е с вградена батерия и зарядно с TYP C:](#️-zigbee-fingerbot-tuya-ts0001-е-добър-избор-със-всички-опции-необходими-за-това-устройство-и-е-с-вградена-батерия-и-зарядно-с-typ-c)
	- [💫 NFC](#-nfc)
		- [ИНСТАЛИРАНЕ НА NFC В HOME ASSISTANT:](#инсталиране-на-nfc-в-home-assistant)

---

## 💥 ИДЕЯ
Електрическите входни брави на повечето градски згради не се оправляват с високо напрежение, а напротив с ниско напрежение което служи за сигнал на електрическата брава за да разбере че някои натиска бутонът в домът си. Всъщност той просто допира кабелите един в друг. Реших да захупя [Zigbee Fingerbot]([figerbot]) който да натиска този бутон и проблемът беше решен, да ама не! Прожините който се слагат на тези ключове за да са винаги в изглючено състояние без натиск са доста корави и [Zigbee Fingerbot]([figerbot]) не успя да се справи!
<br>

Замислих се че след като [Zigbee Fingerbot]([figerbot]) не може да натисне ключът той ще допира кабелите един в друг, точно така както прави и ключът Ви, а по кабелите не тече ток, така че няма да е необходим ел. техник и ще се справя и сам.<br>

> [!CAUTION]
> Въпреки това винаги проверявайте кабелите с мултицет за напрежение!

> Изработих примерна схема за ди си представите какъв трябва да е резултатът:

![shema](/img/shema_HASS-Fingerbot-HFC-Door.png)

| След демонтаца на ключът използвах такива [кабелни съединители]([[klamma]]) за да извадя и двата кабела в страни от ключът. Така ключът остава функционален и [Zigbee Fingerbot]([figerbot]) ще работи. | ![klamma](/img/klamma.png)  |
|-----|-----|

## ⚙️ [Zigbee Fingerbot TUYA TS0001:]([figerbot]) е добър избор със всички опции необходими за това устройство и е с вградена батерия и зарядно с TYP C:

|![Fingerbot](/img/Fingerbot.png)|![Fingerbot option](/img/Fingerbot_option.png)|
|-----|-----|


| **Опция** | **Описание** |
| ----- | ---- |
| **State** | Състояние `ON`/`OFF` — активира или деактивира натискането на бутона.|
| **Battery** | Остатъчен заряд на батерията в проценти (`%`). Обновяването може да отнеме до 24 часа. |
| **Mode** | Работен режим – определя поведението на Fingerbot:<br>• `Click` – Кратко натискане<br>• `Switch` – Превключване между натиснато и освободено<br>• `Program` – Персонализирано поведение (зависи от фърмуера). |
| **Lower** | **Долен лимит на движение** – задава колко надолу се движи рамото при натискане (в %). |
| **Upper** | **Горен лимит на движение** – задава колко се прибира рамото след натискане (в %). |
| **Delay** | **Задържане** – колко време рамото задържа бутона натиснат (в секунди). |
| **Reverse** | Ако е включено, **обръща посоката на движение на мотора** (полезно при обърнат монтаж). |
| **Touch** | Включва или изключва **ръчно активиране чрез докосване** на самото устройство. |
| **Linkquality** | Качество на сигнала (`LQI`) – по-висока стойност означава по-добра Zigbee връзка.|

> Снимки на монтираният вече [Zigbee Fingerbot]([figerbot])
> 
|![img](/img/photo001.jpg)|![img](/img/photo002.jpg)|
|----|----|
|![img](/img/photo003.jpg)|![img](/img/phofo004.jpg)|


## 💫 NFC
Най-пополярните NFCtag съвместими с почти всички устройства са [ntag213]([NFCtag1]) [ntag215]([NFCtag2]), аз предпоръчвам [ntag213]([NFCtag1]) моят телефон работи по добре с него, а и на останалите от семейството.

> [!TIP]
> При избор на NFCtag се уверете че закупувате презаписващи тагове!!!

### ИНСТАЛИРАНЕ НА NFC В HOME ASSISTANT:
NFCtag се инсталира през мобилно устройство и приложението на Home Assistant, моето устройсво е [POCO X3 NFC PRO]([poco]) с инсталиран [HyperOS2]([hyperos])

|От менюто изберете настройки.|Изберете опциите на приложението.|
|----|----|
|![nfc](/img/nfc/nfctag1.png)|![nfc](/img/nfc/nfctag2.png)|

|Вървете на NFCtag.|След като сканирате тага изберете създаване на евент.|
|----|----|
|![nfc](/img/nfc/nfctag3.png)|![nfc](/img/nfc/nfctag4.png)|

|||
|----|----|
|![nfc](/img/nfc/nfctag5.png)|![nfc](/img/nfc/nfctag6.png)|

|От главното меню на HASS вържете на тагове.|Там ще видите новият таг, ще го познаете по ИД-то което видяхме при сканирането.|

|Изберете трите точки в горният край на новият таг и изберете "Нова Автоматизация".| Добавете [Zigbee Fingerbot]([figerbot])|
|----|----|
|![nfc](/img/nfc/nfctag7.png)|![nfc](/img/nfc/nfctag8.png)|


> [!TIP]
> Ако този проект ви е харесъл, [ТУК](https://github.com/Bacard1?tab=repositories) ще намерите още интересни гранилища направени от мен.<br>
> Ако срещате затруднения или имате въпроси не се колебайте да се свържете с мен.

[hyperos]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
[poco]: https://www.mi.com/de/product/poco-x3-pro?srsltid=AfmBOoqKmKAtF-_P0cmo5_mUh5KyV_rqULEeFMbqT99BiuWWyo8BDJRW
[klamma]: https://de.aliexpress.com/item/1005005805414976.html?spm=a2g0o.order_list.order_list_main.212.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[figerbot]: https://de.aliexpress.com/item/1005008341830865.html?spm=a2g0o.order_list.order_list_main.363.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag1]: https://de.aliexpress.com/item/1005007613908773.html?spm=a2g0o.order_list.order_list_main.394.21c85c5f8qzzfj&gatewayAdapt=glo2deu
[NFCtag2]: https://de.aliexpress.com/item/1005006332360160.html?spm=a2g0o.order_list.order_list_main.217.21c85c5f8qzzfj&gatewayAdapt=glo2deu