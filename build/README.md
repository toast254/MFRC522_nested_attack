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

```
pi@raspberrypi:~ $ cd MFRC522_nested_attack/
pi@raspberrypi:~/MFRC522_nested_attack $ make
g++ -c --std=c++11 src/main.cpp -o build/main.o
g++ -c --std=c++11 src/RC522.cpp -o build/RC522.o
g++ -c --std=c++11 src/MFrec.cpp -o build/MFrec.o
gcc -c src/crapto1.c -o build/crapto1.o
gcc -c src/crypto1.c -o build/crypto1.o
g++ build/main.o build/RC522.o build/MFrec.o build/crapto1.o build/crypto1.o -o crack -lpthread -lwiringPi
pi@raspberrypi:~/MFRC522_nested_attack $ ./crack
Recovering keys.. this may take some time
<35.19>Round 1: Found 1448025 possible keys, with most repeated key: 4
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
KEY FOUND TO BE:                11ffffffffff
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Time to crack: 35.19
Timeout
pi@raspberrypi:~/MFRC522_nested_attack $ ./crack
Recovering keys.. this may take some time
<46.7911>Round 1: Found 1460708 possible keys, with most repeated key: 4
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
KEY FOUND TO BE:                11ff22ff43f4
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Time to crack: 46.7911
Timeout
pi@raspberrypi:~/MFRC522_nested_attack $ make clean
rm crack build/main.o build/RC522.o build/MFrec.o build/crapto1.o build/crypto1.o
pi@raspberrypi:~/MFRC522_nested_attack $
```
