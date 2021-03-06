# Parakeet-8266
Прибор совмещающий функции xDrip и Parakeet на основе контроллера ESP8266 с прошивкой NodeMCU.<br>
Вариант реализации Parakeet для системы Dexcom G4 с передачей данных через WiFi сети плюс возможность передавать данные по протоколу BlueTooth.<br>
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
4. BlueTooth модуль HM-10 или HM-11 (при желании использовать прибор как xDrip).
<b>Схема соединения:</b><br>
<br>
VCC Радиомодуля - Контакт 3.3V контроллера<br>
SCLK Радиомодуля - Контакт D5 контроллера<br>
SI Радиомодуля - Контакт D7 контроллера<br>
SO Радиомодуля - Контакт D6 контроллера<br>
CSN Радиомодуля - Контакт D8 контроллера<br>
GDO Радиомодуля - Контакт D1 контроллера (Назначается строкой #define GDO0_PIN в прошивке)<br>
GND Радиомодуля - Контакт GND контроллера (земля)<br>
LEN Радиомодуля - Контакт D1 контроллера (Назначается строкой #define LEN_PIN в прошивке). Можно подключить на контакт 3.3V контроллера (необходимо запитать усилитель слабого сигнала)<br>
VCC модуля BlueTooth - Контакт 3.3V контроллера<br>
GND модуля BlueTooth - Контакт GND контроллера (земля)<br>
TX модуля BlueTooth - Контакт D4 контроллера (Назначается строкой #define RX_PIN в прошивке)<br>
RX модуля BlueTooth - Контакт D3 контроллера (Назначается строкой #define TX_PIN в прошивке)<br>
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
<br>
<b>Настройка прибора:</b><br>
<br>
После включения прибора, первые 2 минуту действует режим конфигурации.<br>
В данном режиме прибор включает точку доступа, которая называетеся Parakeet и запускает WebServer на адресе 192.168.70.1<br>
Подключившись к данной точке доступа можно изменить настройки прибора.<br>
Данные настройки можно поменять и в файле проекта Parakeet-8266.ino:<br>
#define my_wifi_ssid         "ssid" - указать свою точку доступа WiFi<br>
#define my_wifi_pwd          "password" - указать свой пароль для точки доступа WiFi<br>
char transmitter_id[] = "ABCDE"; - указать код своего трансмиттера.<br>
При желании можно изменить адрес облачного сервиса:<br>
#define my_webservice_url    "http://parakeet.esen.ru/receiver.cgi"<br>
и цифровой код для доступа к данным:<br>
#define my_password_code     "12543"<br>
<br>
Но следует помнить, что сохраненные в энергонезависимой памяти настройки имеют более высокий приоритет, чем значения из исходного кода программы.<br>
В программе xDrip+ данный прибор необходимо настраивать как "WiFi Wixel+BT Wixel"<br>
