# Parakeet-8266
Паракит на основе контроллера ESP8266 с прошивкой NodeMCU.<br>
Вариант реализации Parakeet для системы Dexcom G4 с передачей данных через WiFi сети.<br>
<br>
<b>Состав прибора:</b><br>
<br>
1. Радиомодуль на основе чипа Texas Instruments CC2500, желательно с усилителем слабого сигнала.<br>
2. Контроллер на базе чипа ESP8266 с разведенными контактами интерефейса SPI.<br>
Разработка велась и тестировалась но вот таком контроллере:<br>
http://robotdyn.ru/catalog/boards/kontroller_arduino_na_chipe_wifi_esp8266_b_c_32mb_pamyati/ <br>
Но должны работать и вот такие контроллеры:<br>
http://robotdyn.ru/catalog/boards/kontroller_nodem_na_chipe_wifi_esp8266_microusb_p2102/ <br>
И, скорее всего, вот такие:<br>
http://robotdyn.ru/catalog/boards/wifi_kontroller_wemos_d1_mini_na_baze_esp8266_microusb_cp2104_flash_pamyat_8mb_16mb_32mb/ <br>
<br>
<b>Схема соединения:</b><br>
<br>
VCC Радиомодуля - Контакт 3.3V контроллера<br>
SCLK Радиомодуля - Контакт D5 контроллера<br>
SI Радиомодуля - Контакт D7 контроллера<br>
SO Радиомодуля - Контакт D6 контроллера<br>
CSN Радиомодуля - Контакт D8 контроллера<br>
GDO Радиомодуля - Контакт D1 контроллера (Назначается строкой #define GDO0_PIN в прошивке)<br>
GND Радиомодуля - Контакт GND контроллера (земля)<br>
LEN Радиомодуля - Контакт 3.3V контроллера (необходимо запитать усилитель слабого сигнала)<br>
<br>
В качестве источника питания для данных контроллеров проще всего взять недорогой Power Bank и подключить его к разъему microUSB контроллера.<br>
<br>
<br>
<b>Заливка прошивки в прибор:</b><br>
<br>
Для заливки прошивки необходимо установить Arduino IDE:<br>
https://www.arduino.cc/en/Main/Software
<br>
Далее необходимо настроить Arduino IDE для работы с контроллерами на базе чипа ESP8266:<br>
https://github.com/Gorgy70/Parakeet-8266/blob/master/ESP8266.docx
<br>
