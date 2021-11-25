# Как добавить интеграцию TTS Яндекс

[Стартовая страница WiKi](https://github.com/DivanX10/wiki#readme)


## Платный вариант
Для работы интеграции [TTS Яндекс](https://github.com/tayanov/Yandex-tts-speechkit-FIX) в Home Assistant необходимо установить [TTS Яндекс](https://github.com/tayanov/Yandex-tts-speechkit-FIX) в custom_components. Данная интеграция работает только с помощью API ключей. API ключи платные.

## Бесплатный вариант
В этом варианте нужно использовать MPD (Music Player Daemon). Про установку Music Player Daemon читаем [здесь](https://github.com/DivanX10/Openwrt-scripts-for-gateway-zhwg11lm/wiki/Как-настроить-Music-Player-Daemon%3F)

* Создаем файлы с речью с помощью [Yandex SpeechKit](https://cloud.yandex.ru/services/speechkit). 
* На сайте [Yandex SpeechKit](https://cloud.yandex.ru/services/speechkit) пролистайте до "Попробуйте Yandex SpeechKit API". 
* Вписываем любую фразу и сохраняем файл на ПК. 
* Конвертируем формат ogg в mp3. Сделать это можно любым способом. Например можно использовать [онлайн конвертер ogg в mp3](https://audio.online-convert.com/ru/convert/ogg-to-mp3).
* Файл mp3 закидываем в MPD, в папку music
* В Home Assistant запускаем аудиофайл через службу service: media_player.play_media

**Пример**
```
service: media_player.play_media
target:
  entity_id: media_player.aqara_gateway_01
data:
  media_content_type: music
  media_content_id: notification_washing_finished_alena.mp3

```

## lumimqttd

> lumimqttd, это альтернативный вариант lumimqtt, имеет дополнительную функцию, такую как TTS Яндекс

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

Пакет lumimqttd можно скачать [здесь](https://t.me/xiaomi_gw_hack/141963)