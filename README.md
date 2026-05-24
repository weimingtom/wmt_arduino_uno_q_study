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
