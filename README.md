# ESP8266 Wardriving
A compilation of scripts and resources for wardriving on the [ESP8266 WiFi microcontroller](https://www.espressif.com/en/products/socs/esp8266), including data visualization tools in Jupyter Notebook.

Documentation on this page is still in development.

## Components
Any ESP8266-based board should work with the basic required components, but the D1 mini form factor is highly recommended since using modules (such as for SD logging + battery management) can be done using plug-and-play hardware in a small footprint. All linked components are D1 mini compatible. 

**Required Components:**
| Component | Purpose |
| --- | --- |
| ESP8266 | Gather WiFi data & control hardware modules
| SD Reader | Store data that we can analyze with WiGLE / Python |
| GPS Module | Grab geolocation data + timestamp |

**Optional Components:**
| Component | Purpose | 
| --- | --- |
| 128x64 OLED | Get a visual display of WiFi data being captured |
| LiPo Battery | Power your ESP8266 for portable applications |
| Battery Module | Manage power for your ESP8266 w/ a LiPo battery |
| 100K Ω Resistor | Optional to read in battery level w/ the D1 Mini |
   
## Hardware Setup

**SD Reader Module** 
| SD Reader Pin | ESP8266 GPIO | D1 Mini Pin |
| --- | --- | --- |
| MISO | GPIO12 | D6 |
| MOSI | GPIO13 | D7 |
| SCK | GPIO14 | D5 |
| CS | GPIO15 | D8 |

**GPS Module** 
| GPS Pin | ESP8266 GPIO | D1 Mini Pin |
| --- | --- | --- |
| TX | GPIO2 | D4 |
| RX | GPIO0 | D3 |

## Data Visualization Scripts


## Additional Boards Manager URL  https://arduino.esp8266.com/stable/package_esp8266com_index.json

Data Visualization Tutorial: https://www.youtube.com/watch?v=pFHUPs51CRQ

## Code Breakdownn 

Here's a breakdown of the code:

The Arduino sketch written for an ESP8266-based device. It involves using various libraries to perform tasks such as displaying information on an SSD1306 OLED screen, connecting to Wi-Fi networks, reading GPS data using TinyGPS++, and logging network information to an SD card.

Here's a breakdown of the code:

1. Library inclusions:
   - `Adafruit_SSD1306.h`: Library for controlling the SSD1306 OLED display.
   - `ESP8266WiFi.h`: Library for connecting to Wi-Fi networks using the ESP8266 module.
   - `SD.h`: Library for interacting with SD cards.
   - `SoftwareSerial.h`: Library for software-based serial communication.
   - `TinyGPS++.h`: Library for parsing NMEA data from GPS modules.
   - `TimeLib.h`: Library for time-related functions.

2. Definitions and global variables:
   - `UTC_offset`: The offset in hours from UTC time to the local time zone (in this case, PDT, which is UTC-7).
   - `SD_CS`: The pin number for the chip select line of the SD card module.
   - `logFileName`: The name of the log file to be created on the SD card.
   - `networks`: A counter variable to keep track of the number of Wi-Fi networks found.
   - `LOG_RATE`: The time interval (in milliseconds) for logging network information.
   - `currentTime`: A character array used to store the current time.

3. Setup function:
   - Initializes the serial communication for debugging purposes.
   - Sets up the SSD1306 display.
   - Configures Wi-Fi in station mode and disconnects any previous connections.
   - Initializes the SD card and checks if it is present. If not found, it halts the execution.
   - Initializes the software serial communication with the GPS module.
   - Waits for the GPS module to provide a valid fix.
   - Displays the GPS coordinates on the OLED screen.
   - Clears the display.

4. `lookForNetworks` function:
   - Updates the current time on the OLED display.
   - Draws lines to separate the time display from the network information.
   - Scans for available Wi-Fi networks.
   - If networks are found, it loops through each network, updates the OLED display, and logs the BSSID and SSID of the network to the SD card.

 
Updates the current time on the OLED display.
Draws lines to separate the time display from the network information.
Scans for available Wi-Fi networks.
If networks are found, it loops through each network, updates the OLED display, and logs the BSSID and SSID of the network to the SD card.
