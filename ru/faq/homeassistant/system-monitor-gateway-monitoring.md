# System Monitor   мониторим шлюз

С помощью интеграции System Monitor мы можем мониторить шлюз, знать его текущее состояние, нагрузку на процессор, свободный объем памяти, сколько места осталось на шлюзе и т.д. более подробнее читаем про интеграцию System Monitor [здесь](https://www.home-assistant.io/integrations/systemmonitor/)

![System Monitor](https://github.com/DivanX10/Openwrt-scripts-for-gateway-zhwg11lm/blob/main/image/system%20monitor.JPG)

Для работы данной интеграции необходимо установить пакет `python3-psutil`. Данный пакет ставим через LuCI

![python3-psutil](https://github.com/DivanX10/Openwrt-scripts-for-gateway-zhwg11lm/blob/main/image/install%20python3-psutil.jpg)

***

[Скачайте архивный файл](https://github.com/home-assistant/core/tags) соответствующий вашей версии Home Assistant и распакуйте из архива папку `systemmonitor`. Полный путь к папке `core-год.месяц.число.zip\core-год.месяц.число\homeassistant\components\systemmonitor` и копируем папку `systemmonitor` в /usr/lib/python3.9/site-packages/homeassistant-XXXX.XX.XX-py3.9.egg/homeassistant/components, где homeassistant-XXXX.XX.XX-py3.9.egg это версия вашего Home Assistant

Более подробнее читаем статью [Как установить недостающий компонент для интеграции Home Assistant?](https://github.com/DivanX10/Openwrt-scripts-for-gateway-zhwg11lm/wiki/Как-установить-недостающий-компонент-для-интеграции-Home-Assistant%3F)


***
Добавим строки в `configuration.yaml` расположенный по пути `/etc/homeassistant/configuration.yaml`. Ниже мой рабочий пример и мне этого достаточно, но вы можете указать свои сенсоры согласно документации интеграции [System Monitor](https://www.home-assistant.io/integrations/systemmonitor/)

> Важно! Сенсор температуры я взял с пакета `lumimqttd` (читаем ниже).

```
# Отображение системных данных: загрузка процессора, занято место на диске, свободно ОЗУ, последняя загрузка.
sensor:
  - platform: systemmonitor
    resources:
      - type: disk_use_percent
        arg: /
      - type: disk_free
        arg: /
      - type: memory_free
      - type: memory_use_percent
      - type: processor_use
      - type: last_boot     
      - type: ipv4_address
        arg: wlan0
      - type: load_1m
```


## lumimqttd
> Пакет lumimqttd, это отдельный пакет для управления подсветки шлюза, а также выводит температуру процессора и имеет датчик света. Пока не имеет сенсора кнопки, возможно в будущем добавят такую опцию. lumimqtt и lumimqttd могут работать вместе и будут дополнять друг друга

**Что умеет делать lumimqttd?**
```
В нем есть:
# поддержка 🤖 auto discovery для homeassistant, 
# можно управлять светодиодами 🎃 
# получать данные освещенности 👁
# проигрывать звук через mqtt  🦻( ссылка или генерация TTS🗣)  
# управлять громкостью каналов ( с обратной связью и получением текущего значения громкости )
# отправка температуры процессора по mqtt
```

Пакет lumimqttd можно скачать [здесь](https://t.me/xiaomi_gw_hack/144897)
