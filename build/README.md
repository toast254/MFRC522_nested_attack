# Mifare Classic Nested Attack

This attack recovers unknown keys from a Mifare Classic PICC (RFID Tag) if only there is a block with a known key. This attack won't be able to recover keys if there is not a known key. Also this attack only works with **not hardened** Mifare Classic tags. Hardened tags may have 7 byte UID and responds ATQA command with **"ATQA (SENS_RES): 00  44"** it may have same SAK with the attackable ones which is **"SAK (SEL_RES): 08"**.

## Build

* Write raspian image to SD card for Raspberry Pi (2017-01-11-raspbian-jessie-lite.img)
* Connect MFRC522 PCD (RC522 Module) to Raspberry (refer RC522.h)
* Install wiringPi (http://wiringpi.com/download-and-install/)
* Enable SPI interface (raspi-config)
* Clone this repo
* Configure attack vectors (block with known key, attack addr) on main.cpp
* make