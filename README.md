# ATEM Tally Control for M5StickC-Plus ( Clarity / BAAElectronics )
## Building from Source (Recommended for Updated Libraries)
* Download the required libraries into your Arduino libraries folder
   - [(M5StickCPlus.h)](https://github.com/m5stack/M5StickC-Plus)
   - [(SkaarhojPgmspace.h)](https://github.com/kasperskaarhoj/SKAARHOJ-Open-Engineering/tree/master/ArduinoLibs/SkaarhojPgmspace)
   - [(ATEMbase.h)](https://github.com/kasperskaarhoj/SKAARHOJ-Open-Engineering/tree/master/ArduinoLibs/ATEMbase)
   - [(ATEMstd.h)](https://github.com/kasperskaarhoj/SKAARHOJ-Open-Engineering/tree/master/ArduinoLibs/ATEMstd)
* Your folder structure should look like this
   - Tally
     - Tally.ino
     - libraries/
       - M5StickCPlus/
         - (Uncompressed files of M5StickCPlus.h here)
       - SkaarhojPgmspace/
         - (Uncompressed files of SkaarhojPgmspace.h here)
       - ATEMbase/
         - (Uncompressed files of ATEMbase.h here)
       - ATEMstd/
         - (Uncompressed files of ATEMstd.h here)
* Follow the instructions below on how to prepare the Arduino IDE
## Downloading Pre-Assembled Version (Not Recommended)
* Download from [Releases](https://github.com/clarityam/ATEM_Tally_Control-M5StickCPlus/releases)
   - Recommended to Build from Source for Updated Libraries
* Follow the instructions below on how to prepare the Arduino IDE
## Preparing the Arduino IDE
* Download the Arduino IDE from [Arduino](https://www.arduino.cc/en/software)
* Add the following board URLs to your Board Manager (Preferences -> Additional Board Manager URLs)
   - https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/arduino/package_m5stack_index.json
   - https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json
* Set your sketchbook location (Preferences -> Sketchbook Location) to the root folder once you download/compile the project. This is so the Arduino IDE can find the libraries.
* Connect your M5StickCPlus to your device and select the board (M5StickCPlus) and the port (COM#) on the top of the IDE
* Follow the instructions below to adjust the project
## Adjusting the project settings (Tally.ino)
   - Required Adjustments:
       - (Line 26) IPAddress switcherIp(0, 0, 0, 0); // Change this to your ATEM's IP Address (Static Recommended)
       - (Line 29) const char* ssid = "network"; // Change this to your Network's SSID
       - (Line 30) const char* password = "password"; // Change this to your Network's Password (Blank if none)
   - Optional Adjustments (Recommended to leave as is):
       - (Line 33) #define AUTOUPDATE_ORIENTATION 1 // Disable this for no orientation changes
       - (Line 37) #define previewLED 25 // Pinout for Green (Camera in Preview)
       - (Line 38) #define bothLED 0 // Pinout for Blue (Camera in Preview & Program)
       - (Line 39) #define programLED 26 // Pinout for Red (Camera in Program)
* At the top of the IDE, click the Arrow once finished (Upload) and allow some time for the project to compile and transfer
   - Optional but Recommended: Set "Erase All Flash Before Sketch Upload" to 'Enabled' (Tools -> Erase All Flash Before Sketch Upload)
## Adding the Multi-Colored 4 PIN LED ( BAAElectronics )
* Ensure the RGB LED being used is of the common cathode type (meaning all cathodes of each emitter are tied together in a common ground). Check your LED's datasheet for the proper pinout. A common pin order is RED, GROUND (longest leg), GREEN, BLUE.
   - Connect each anode pin to the M5's G0, G25, and G26 outputs as shown in the schematic below.
       - G0 = blue "camera in preview/program" color by default.
       - G25 = green "camera in preview only" by default.
       - G26 = red "camera in program only" by default.
   - Connect the common cathode pin to the M5's GND header.
![Screenshot 2023-09-15 at 12 28 54 PM](https://github.com/clarityam/ATEM_Tally_Control/assets/40682937/fec64100-079e-4b4c-96df-2b2482f5ecf0)
* For a common anode configuration, connect each cathode to G0, G25, and G26. Connect the anode to the M5's 3.3v output. In Tally.ino, flip the booleans of each LED parameter passed to drawLabel() so that when a pin is held HIGH, the voltage across that emitter is zero; otherwise, a pin held LOW will apply a 3.3v differential to the emitter, causing current to flow and the emitter to light.
* DISCLAIMER: The common anode configuration has not been tested and is not supported by the current release of this project. Try at your own discretion. Common cathode RGB LEDs are cheap.
## Troubleshooting
* A fatal error occurred: Failed to connect to ESP32: No serial data -
  - Attempt the following:
    - Long press the power button, when the Logs show 'Connecting.....'
    - Set the Baud Rate to 115200
    - Bridging the GND to G0 connector
    - If not solved, contact the store you purchased your unit from
