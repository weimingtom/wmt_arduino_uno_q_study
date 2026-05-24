# wmt_arduino_uno_q_study
[WIP] My Arduino Uno Q study

## Start examples
* https://docs.arduino.cc/tutorials/uno-q/debian-guide/
* adb shell
* arduino-app-cli app list
* arduino-app-cli app start examples:blink

## Start classical Arduino blink program  
* https://docs.arduino.cc/software/app-lab/cli/cli/
* https://docs.waveshare.net/Arduino-UNO-Q-02016/Hardware-Interfaces
* https://docs.arduino.cc/resources/pinouts/ABX00162-full-pinout.pdf
* https://docs.arduino.cc/tutorials/uno-q/user-manual/
* (search Digital Pins)
* adb shell
* $ arduino-app-cli app new "test"
* (App created successfully: /home/arduino/ArduinoApps/test (ok))
* $ exit
* adb pull /home/arduino/ArduinoApps/test .
* (For Windows) explorer .
* (For Windows) notepad test\sketch\sketch.ino
```
void setup() {
  // put your setup code here, to run once:
 pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```
* adb push test /home/arduino/ArduinoApps/.
* adb shell
* $ cd ArduinoApps/test/
* $ cat sketch/sketch.ino
* $ arduino-app-cli app start .
* ([ERROR] App "Blink Led" Is Running)
* $ sudo reboot
* adb shell
* $ cd ArduinoApps/test/
* $ arduino-app-cli app start .
* (App "test" started successfully)
* $ arduino-app-cli app stop .
* $ nano sketch/sketch.ino
* (modify delay(1000) to delay(100))
* $ arduino-app-cli app start .

## Use arduino-cli to compile and upload blink program  
* https://arduino.github.io/arduino-cli/1.5/getting-started/
* https://arduino.github.io/arduino-cli/1.5/commands/arduino-cli_board_details/
* $ arduino-cli board list
```
No boards found.
```
* $ arduino-cli core list
```
ID             Installed Latest Name
arduino:zephyr 0.55.0    0.55.0 Arduino UNO Q Board
```
* $ arduino-cli board list
(**NOTE: It's not /dev/ttyACM1 Serial Port type**)
```
Port        Protocol Type         Board Name    FQBN                Core
192.168.1.2 network  Network Port Arduino UNO Q arduino:zephyr:unoq arduino:zephyr
```
* $ arduino-cli board details -b arduino:zephyr:unoq
```
Board name:                Arduino UNO Q
FQBN:                      arduino:zephyr:unoq
Board version:             0.55.0

Official Arduino board:    ✔

Identification properties: pid=0x0078
                           vid=0x2341

Package name:              arduino
Package maintainer:        Arduino
Package URL:               https://downloads.arduino.cc/packages/package_index.tar.bz2
Package website:           https://www.arduino.cc/
Package online help:       https://www.arduino.cc/en/Reference/HomePage

Platform name:             Arduino UNO Q Board
Platform category:         Arduino
Platform architecture:     zephyr
Platform URL:              https://downloads.arduino.cc/cores/zephyr/ArduinoCore-zephyr_unoq-6544208c.tar.bz2
Platform file name:        ArduinoCore-zephyr_unoq-6544208c.tar.bz2
Platform size (bytes):     6468189
Platform checksum:         SHA-256:e3cbf7177af9ba38b1a900ee038741baca536b6bb5b81d1d411ea7f1671b7035

Required tool: SiliconLabs:openocd                0.12.0-arduino1-static
Required tool: arduino:adb                        32.0.0
Required tool: arduino:bossac                     1.9.1-arduino2
Required tool: arduino:dfu-util                   0.11.0-arduino5
Required tool: arduino:gen-rodata-ld              0.1.1
Required tool: arduino:remoteocd                  0.0.4-rc.4
Required tool: arduino:sync-zephyr-artifacts      0.2.1
Required tool: arduino:zephyr-sketch-tool         0.3.0
Required tool: zephyr:arm-zephyr-eabi             0.16.8

Option:        Link mode                                                   link_mode
               Dynamic                            ✔                        link_mode=dynamic
               Static                                                      link_mode=static
Option:        Startup mode                                                wait_linux_boot
               Wait for Linux                     ✔                        wait_linux_boot=yes
               Immediate                                                   wait_linux_boot=no
               Wait for App                                                wait_linux_boot=app
Programmers:   ID                                 Name
               cmsis-dap                          ARM CMSIS-DAP compatible
               jlink                              JLink
               openocd                            OpenOCD
```
* $ arduino-cli sketch new MyFirstSketch
```
Sketch created in: /home/arduino/MyFirstSketch
```
* $ nano /home/arduino/MyFirstSketch/MyFirstSketch.ino
```
void setup() {
pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
digitalWrite(LED_BUILTIN, HIGH);
delay(5000);
digitalWrite(LED_BUILTIN, LOW);
delay(5000);
}
```
* $ cd /home/arduino/MyFirstSketch
* $ arduino-cli compile -b arduino:zephyr:unoq .
* (or --fqbn)
```
Please install the Arduino_RouterBridge library from the Library Manager for)
```
* $ arduino-cli lib search Arduino_RouterBridge
* $ arduino-cli lib install Arduino_RouterBridge
```
Sketch uses 18564 bytes (2%) of program storage space. Maximum is 786432 bytes.
Global variables use 9504 bytes (7%) of dynamic memory, leaving 121568 bytes for local variables. Maximum is 131072 bytes.
```
* (rebuild but not upload) $ arduino-cli compile -b arduino:zephyr:unoq --clean --verbose .
* (not rebuild only upload) $ arduino-cli upload -b arduino:zephyr:unoq .
* $ arduino-cli compile -b arduino:zephyr:unoq --verbose --upload .
