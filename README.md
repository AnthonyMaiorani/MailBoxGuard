## LoRa MailBox Sensor and LoRa Gateway



==============================

### Made 3 firmware for the LoRa Gateway
1. `LoRa_Gateway_OLED.ino` "For offline use" Display turns on and shows that there is a new letter in the mailbox "number of letters", "signal strength" and "Battery State". After taking your mail, you need to press the reset button on the gateway.
2. `LoRa_Gateway_WhatsApp.ino` Sends a message to WhatsApp "You Have New Mail"
3. `LoRa_Gateway_MQTT.ino` Sends a row message and RSSI to MQTT Server

# Gateway Configuration

### Select Board Version

- Change the BOARD definition in `board.h` according to the your board Version " 1 = ON / 0 = OFF ".
 ```
 #define LORA_V1_0_OLED  0
 #define LORA_V1_2_OLED  0
 #define LORA_V1_6_OLED  0
 #define LORA_V2_0_OLED  1
 ```
### LoRa Configuration

- The settings in the gateway and in the sensor must match.
```
#define SignalBandwidth 125E3
#define SpreadingFactor 12
#define CodingRate 8
#define SyncWord 0xF3
#define PreambleLength 8
#define TxPower 20
float BAND = 868E6; // 433E6 / 868E6 / 915E6 /
```
### New Mail Code Configuration

- In `LoRa_Gateway_OLED.ino` and `LoRa_Gateway_WhatsApp.ino`
```
String NewMailCode = "REPLACE_WITH_NEW_MAIL_CODE"; // For Example "0xA2B2";
String LowBatteryCode = "REPLACE_WITH_LOW_BATTERY_CODE"; // For Example "0xLBAT";
```


### WiFi Configuration
- In `LoRa_Gateway_MQTT.ino` and `LoRa_Gateway_WhatsApp.ino`
```
const char* ssid = "Your_WIFI_SSID";
const char* password = "Your_WIFI_password";
```
### MQTT Configuration

- Only in `LoRa_Gateway_MQTT.ino`
```
const char* mqtt_username = "Your_mqtt_username";
const char* mqtt_password = "Your_mqtt_password";
const char* mqtt_server = "Your_mqtt/homeassistant server IP";
const int mqtt_port = 1883;

```
# MailBox Sensor Configuration

### MailBox LoRa Configuration
- In `Mailbox_Guard_Sensor.ino`
```
  LoRa.setSignalBandwidth(125E3);         // signal bandwidth in Hz, defaults to 125E3
  LoRa.setSpreadingFactor(12);                 // ranges from 6-12,default 7 see API docs
  LoRa.setCodingRate4(8);        // Supported values are between 5 and 8, these correspond to coding rates of 4/5 and 4/8. The coding rate numerator is fixed at 4.
  LoRa.setSyncWord(0xF3);                     // byte value to use as the sync word, defaults to 0x12
  LoRa.setPreambleLength(8);       //Supported values are between 6 and 65535.
  LoRa.disableCrc();                          // Enable or disable CRC usage, by default a CRC is not used LoRa.disableCrc();
  LoRa.setTxPower(20);                // TX power in dB, defaults to 17, Supported values are 2 to 20
```

### New Mail and Low Battery code
- In `Mailbox_Guard_Sensor.ino`
```
String NewMailCode = "REPLACE_WITH_NEW_MAIL_CODE"; // For Example "0xA2B2";
String LowBatteryCode = "REPLACE_WITH_LOW_BATTERY_CODE"; // For Example "0xLBAT";
```
