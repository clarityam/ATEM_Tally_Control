# ATEM Tally Control for M5StickCPlus (Clarity)

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
* Follow the instructions below on how to Adjust the Project
## Downloading Pre-Assembled Version (Not Recommended)
* Download from [Releases](https://github.com/clarityam/ATEM_Tally_Control-M5StickCPlus/releases)
   - Recommended to Build from Source for Updated Libraries
* Follow the instructions below on how to Adjust the Project
## How to Adjust the Project to your settings (Tally.ino)
   - Required Adjustments:
       - (Line 26) IPAddress switcherIp(0, 0, 0, 0); // Change this to your ATEM's IP Address (Static Recommended)
       - (Line 29) const char* ssid = "network"; // Change this to your Network's SSID
       - (Line 30) const char* password = "password"; // Change this to your Network's Password (Blank if none)
   - Optional Adjustments (Recommended to leave as is):
       - (Line 33) #define AUTOUPDATE_ORIENTATION 1 // Disable this for no orientation changes
       - (Line 37) #define previewLED 25 // Pinout for Green (Camera in Preview)
       - (Line 38) #define bothLED 0 // Pinout for Blue (Camera in Preview & Program)
       - (Line 39) #define programLED 26 // Pinout for Red (Camera in Program)
