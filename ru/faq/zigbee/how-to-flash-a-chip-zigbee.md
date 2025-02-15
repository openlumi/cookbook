---

categories:
- zigbee

software:
- jntools
---
# Как перепрошить чип ZigBee?

**1)** Скачать нужную прошивку

* Скачиваем последнюю прошивку [здесь](https://github.com/openlumi/ZiGate/releases)

Обратите внимание на именование прошивок для zigbee2mqtt, где:
* **8ede\3535\f0dd** - версия прошивки
* **JN5168\JN5169** - версия чипа zigbee
* **COORDINATOR** - работа шлюза в режиме координатора
* **115200\1000000** - скорость передачи в бодах (baudrate)
* **GP_Proxy** - включена поддержка green power и 242 endpoint 

> Важно! Про GP_Proxy. Так как у автора прошивки zigbee2mqtt нет девайсов с поддержкой green power и нет тестеров, то поддержка в адаптере не реализована. Если вы перепрошьете чип zigbee прошивкой с GP_Proxy, то стабильная работа не гарантируется и могут наблюдаться частые отвалы и проблемы с сопряжением. Рекомендую использовать прошивку без GP_Proxy


***


**Например разберем прошивку ZigbeeNodeControlBridge_f0dd_JN5168_COORDINATOR_1000000.bin**
Прошивка версии f0dd для чипа с версией JN5168. Шлюз будет работать в режиме координатора. Скорость передачи 1000000

**Например разберем прошивку ZigbeeNodeControlBridge_3535_JN5168_COORDINATOR_115200.bin**
Прошивка версии 3535 для чипа с версией JN5169. Шлюз будет работать в режиме координатора. Скорость передачи 115200

**Например разберем прошивку ZigbeeNodeControlBridge_3535_JN5168_GP_Proxy_COORDINATOR_115200.bin**
Прошивка версии 3535 для чипа с версией JN5168. Шлюз будет работать в режиме координатора. Скорость передачи 115200. Включена поддержка green power

**Например разберем прошивку ZigbeeNodeControlBridge_f0dd_JN5169_COORDINATOR_1000000_DEBUG_LOG.bin**
Прошивка версии f0dd для чипа с версией JN5169. Шлюз будет работать в режиме координатора. Скорость передачи 1000000. Ведет журналирование отладочной информации


***

**2)** Открываем в LuCI страницу Zigbee Tools. System => Zigbee Tools

Порядок действии перед прошивкой чипа Zigbee:
* Остановить службу zigbee2mqtt (если служба zigbee2mqtt запущена, то запущенная служба zigbee2mqtt не даст перепрошить чип zigbee )
* Стереть данные чипа Zigbee, нажимаем на ErasePDM
* Выбрать нужный baudrate для прошивки
* Загрузить прошивку
* При желании можно повторно стереть данные чипа Zigbee, нажимаем на ErasePDM (делать не обязательно, но хуже не будет)
* В конфигурационном файлике `configuration.yaml` расположенному по пути `/etc/zigbee2mqtt/configuration.yaml` указать нужный baudrate 115200\1000000. 
* Запустить службу zigbee2mqtt

> Важно! Если есть проблема с запуском zigbee2mqtt, то читаем: [Установил zigbee2mqtt. Не работает веб страница zigbee2mqtt](https://github.com/DivanX10/Openwrt-scripts-for-gateway-zhwg11lm/wiki/Установил-zigbee2mqtt.-Не-работает-веб-страница-zigbee2mqtt)


![image](https://user-images.githubusercontent.com/64090632/145588430-f65c3ff8-66db-4090-81e6-6b8efbb4330e.png)


***
### Примеры команд
**Просмотреть полный список команд**
```
/etc/init.d/zigbee2mqtt
```
**Остановить службу zigbee2mqtt**
```
/etc/init.d/zigbee2mqtt stop
```
**Запустить службу zigbee2mqtt**
```
/etc/init.d/zigbee2mqtt start
```

**Перезагрузить службу zigbee2mqtt**
```
/etc/init.d/zigbee2mqtt restart
```

## Справочная информация

**У меня девайсы zigbee часто отваливаются от шлюза, что делать?**

Если вы перепрошили чип прошивкой с GP_Proxy, то необходимо перепрошить чип zigbee без GP_Proxy.
