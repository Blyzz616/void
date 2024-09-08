# Mørk natt

Mørk natt is Norwegian that translates into "Dark night"

https://github.com/user-attachments/assets/9e299e63-a6f7-4f7b-ad3c-f0894cde03f0

(it's just audo)

The Plan:

# Bedside Alarm Clock Design

## Requirements:

1. **No lights**: The alarm clock should not emit any light to ensure it doesn’t disturb sleep.
2. **Decent audio**: Must have a good quality speaker for the alarm sound.
3. **Externally powered**: The clock will be plugged into an external power source, but it must retain power in the event of a power outage.
4. **Traditional digital alarm clock shape**:
   - **Cube-like design**: Wide and deep but not tall, ensuring stability and preventing it from falling over.
   - **Large top surface**: Large enough to accommodate a snooze button and an off button, easily accessible.

## Components and Features:

### 1. **Core System**: 
   - [**Raspberry Pi Zero 2 W**](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/): The Raspberry Pi will serve as the brain of the clock, handling time management, alarms, and the display.  
     ![zero2-close-up](https://github.com/user-attachments/assets/1bbfd786-e964-4cbd-b4bd-3c47bec7325b)

### 2. **Display**:
   - [**E-Paper Display**](https://www.waveshare.com/product/displays/e-paper/5.79inch-e-paper-module.htm):
     - Display size: `139.00 × 47.74mm` (972px x 272px).
     - **Display type**: E-paper to ensure no light emission.
     - **Connection**: Requires a controller board to connect the display to the Pi and will need to be hardwired.  
       ![5 79inch-e-paper-module-1-removebg-preview](https://github.com/user-attachments/assets/83a63686-138e-4ffe-9f68-e9134ac72881)  
       ![5 79inch-e-paper-module-3-removebg-preview](https://github.com/user-attachments/assets/cdcb0e65-c2d6-47da-a422-c1f1ed14ce3a)

### 3. **Audio**:
   - [**ReSpeaker 2-Mics Pi HAT**](https://wiki.seeedstudio.com/ReSpeaker_2_Mics_Pi_HAT/): This HAT will handle the audio for the alarm sound. It has built-in microphones and a speaker output to provide decent quality sound.  
     ![107100001_SPL-removebg-preview](https://github.com/user-attachments/assets/c64082bd-a4f5-4f15-9152-33775e9936a5)


### 4. **Power Backup**:
   - [**Uninterruptible Power Supply UPS HAT for Raspberry Pi Zero**](https://www.pishop.ca/product/uninterruptible-power-supply-ups-hat-for-raspberry-pi-zero-stable-5v-power-output/): This will ensure that the clock retains power in the event of a power outage, so it doesn't lose track of the time or alarms.  
     ![ups-hat-c-1__96622-removebg-preview](https://github.com/user-attachments/assets/4cb87744-dbcd-42ed-bd1c-4d8ad504965f)  
     ![61H0DgMoGVS _AC_UF894_1000_QL80_-removebg-preview](https://github.com/user-attachments/assets/69e05c4f-fb5e-4efd-b9fc-86a1f38118ea)



### 5. **Buttons/Switches for User Control**:
   - **6 Momentary, Non-Latching Buttons**:
     1. **Button A**: Snooze the alarm.
     2. **Button B**: Turn the alarm off.
     3. **Button C**: Toggle the display between showing the current time and the alarm time.
     4. **Button D**: Factory reset.
     5. **Button E (+)**: Increase the alarm time when setting or adjusting it.
     6. **Button F (-)**: Decrease the alarm time when setting or adjusting it.
   
   - **Rocker or Sliding Switch**: To enable or disable all alarms.

### 6. **Time Control**:
   - **NTP Sync**: The clock will sync with Network Time Protocol (NTP) if internet is available during setup.
   - **Manual Time Adjustment**: If no internet is available, Buttons E and F will be used to manually set the time.

### Expected Investment:
   
   | Item  | Cost |
   | ------------- | ------------- |
   | [Raspberry Pi Zero 2 W ](https://www.pishop.ca/product/raspberry-pi-zero-2-w/?src=raspberrypi) | C$: **21.00** |
   | [ePaper Display](https://www.waveshare.com/product/displays/e-paper/5.79inch-e-paper-module.htm) | C$ **38.00** |
   | [ReSpeaker 2-Mics Pi Hat](https://www.seeedstudio.com/ReSpeaker-2-Mics-Pi-HAT.html) | C$ **17.50** |
   | [Pi UPS](https://www.pishop.ca/product/uninterruptible-power-supply-ups-hat-for-raspberry-pi-zero-stable-5v-power-output/) | C$ **33.95** |
   | Enclosure: 3D printed. Probably going to go through multiple iterations so maybe around | C$ **40.00** |
   | SD card: I'll probably use 16Gb cards which go for under | C$ **10.00** |
   | [Power Supply](https://www.pishop.ca/product/usb-c-power-supply-5-1v-3-0a-black-ul-listed/) | C$ **9.95** |
   | [USB-C enclosure support](https://www.mouser.ca/ProductDetail/CUI-Devices/UJ20-C-H-G-SMT-TR?qs=vvQtp7zwQdMB%2FjSfD6wTAw%3D%3D) | C$ **2.02** | 
   | Buttons, Switches, jumper cables | C$ **15.00** |
   | Shipping not included in any prices maybe another ? | C$ **60.00** |


   *Including 12% tax, for 2x, no-light, fully customisable, bed-side alarm clocks, that should bring the total to around C$ **420***
     
That's of course not counting the time bulding, designing the enclosure and doing all the coding - but that's where the fun comes in!

# Wi-Fi Setup Flowchart

## 1. On Boot/Power-On:
- **Check for saved Wi-Fi network:**
  - **If connected:** Proceed with normal operation (NTP sync, locale set via timezone).
  - **If not connected:**
    - **Step 1: Scan for available Wi-Fi networks (APs).**
      - **If no APs are found:**
        - Display message: `"No Wi-Fi available. Press and hold Button B for 3 seconds to use offline mode."`
        - If Button B is held for 3 seconds, disable Wi-Fi and allow the user to set the time manually using Buttons E (+) and F (-).
        - **Otherwise**, keep scanning for available Wi-Fi networks every minute.
      - **If APs are found:**
        - **Step 2: Display option to press Button B for 3 seconds to use Offline Mode or press Button C to connect to Wi-Fi.**
        - **If Button B is long-pressed:** Disable Wi-Fi, enter offline mode, and allow time setup manually.
        - **If Button C is pressed:** Proceed with Wi-Fi setup using a mobile device.

## 2. Wi-Fi Setup using Web Interface (if Button C is pressed):
- **Step 3: Enable AP mode on the Pi and generate a QR code** showing the clock's AP credentials (random ESSID and password).
- **Step 4: Display a message on the e-paper screen**: `"Scan QR code to connect to the clock’s Wi-Fi."`
  - The user connects to the clock's Wi-Fi on their mobile device.
- **Step 5: Once connected to the clock's Wi-Fi**, show the following options on a web interface served by the Pi:
  1. **Select Wi-Fi from available networks** (list acquired during scan) and enter password.
  2. **Manually enter Wi-Fi name and password** (for hidden networks).
  3. **Use WPS** (if supported).
  4. **Go into Offline Mode** (disable Wi-Fi, allow manual time setup).

## 3. Time and Locale Setup:
- **Step 6: After Wi-Fi is set up (or in offline mode),** prompt the user to set the locale (timezone).
  - If connected to Wi-Fi, the clock will automatically try to set the timezone based on locale information acquired via NTP.
  - **If no Wi-Fi:** Show a list of general timezone options (e.g., UTC, PST, EST, etc.) that can be selected using Buttons E (+) and F (-), or let the user enter the timezone manually via the web interface during offline mode setup.

## 4. Fallback for Hidden APs or WPS:
- If the user selects **hidden AP** or **WPS**, allow manual input of AP name/password via the web interface or guide the user through WPS setup (if supported by their router).

## 5. Completion:
- **Step 7: On successful connection to Wi-Fi or manual time setup** (in offline mode), display the time and any alarms set on the e-paper screen.
  - If Wi-Fi is connected, automatically sync the time via NTP based on the selected locale.

# Daily Operation

## 1. **Clock Update**:
- The clock will update once per minute and show the current time on the e-paper display.

## 2. **Set Up a New Alarm** - Controlled with button C

#### 2.1. **Short Press Button C**:
- The first alarm time will be displayed.
- Use **Buttons E (+)** and **F (-)** to adjust the alarm time.
- Press **Button C** again to either save or proceed:
  
##### 2.1.1. **Short Press While Alarm Time is Displayed**:
- Saves the current alarm time and either:
  - **2.1.1.1**: Moves to the next alarm (if one exists), and **2.1.1** is repeated.
  - **2.1.1.2**: If no next alarm exists, it starts setting up a new alarm. The initial time is set to 12:00, which can be adjusted using **+** or **-** buttons.

##### 2.1.2. **Long Press While Alarm Time is Displayed**:
- Saves the current alarm and exits back to the clock display showing the current time.

### 2.2. **Long Press Button C** While Time is Displayed:
- Enables Wi-Fi Access Point (AP) mode and displays a QR code for easy mobile connection.
- The mobile web interface will allow users to:
  - Add new alarms.
  - Edit existing alarms.
  - Delete alarms.

## 3. **Alarm Operation**:

### 3.1. **While an Alarm is Going Off**:
- **Button A**: Snoozes the alarm for 5 minutes.
  - The default snooze period can be changed via the mobile web interface or on a per-alarm basis.
- **Button B**: Stops the alarm.

## 4. **Factory Reset**:
- **Button D** (recessed and hidden behind a small hole) will act as a reset button.
- Pressing **Button D** will restore the clock to factory defaults.

# Web Interface Design for Bedside Alarm Clock

## Main Menu Options:
1. **Audio Streaming Service Setup**:
   - Add and save a streaming service for audio playback (e.g., music, alarms).
   - Supported streaming services:
     - **Spotify**
     - **Apple Music**
     - **Pandora**
     - **Deezer**
     - **Google Play Music**
     - **TuneIn Radio**
     - **SoundCloud**
   - Allow the user to authenticate with their account for the selected service.

2. **Alarm Management**:
   - Add, edit, or delete alarms.
   - Set custom times, tones, or actions for each alarm.

3. **Alarm Tone Options**:
   - Choose a built-in alarm tone (default sounds).
   - Upload a custom audio clip (e.g., MP3, WAV files).
   - Select which streaming service to use as the alarm source (stream specific playlists, songs, or radio channels).
   
4. **System Usage Opt-In**:
   - Allow users to **opt-in** to a system that tracks how many clocks are in service, using IP addresses to estimate location.
   - **Disabled by default**.

5. **Wi-Fi Configuration**:
   - Reconfigure Wi-Fi settings:
     - Scan for available networks.
     - Input new SSID and password.
   
6. **System Management**:
   - **Reboot Clock**: Restart the system if needed.
   - **Restore Factory Defaults**: Reset all settings to default, erasing user data.

7. **Easter Eggs**:
   - Add some fun hidden features (e.g., small games, quirky sounds, or hidden custom modes).
   - Consider adding:
     - Random messages or jokes when accessing certain settings.
     - Special audio clips unlocked after a certain time or during holidays.
     - Hidden themes for the web interface.

## Additional Features:
1. **Locale and Time Zone Setup**:
   - Let users configure the clock's locale, time zone, and daylight saving settings, especially useful when the clock is offline.

2. **Battery Management**:
   - Display the current battery status or power source.
   - Notify users of low power or if the clock is running on UPS backup.

3. **NTP Sync Toggle**:
   - Option to toggle NTP syncing (time synchronization with the internet).
   - Allow manual time adjustment if NTP is disabled.

4. **Alarm Snooze Customization**:
   - Customize snooze intervals for each alarm (e.g., 5 minutes, 10 minutes, 15 minutes).
   - Maybe even change alarm tone based on how many times the snooze has been hit

## Additional Considerations:
- **User Feedback**:
  - Add a "Feedback" option for users to report bugs or suggest features.
  - Implement an optional user poll to vote for future features.
  
- **Integration with Smart Home Devices**:
  - Future option to integrate with platforms like **Google Home**, **Amazon Alexa**, or **IFTTT** to control alarms and music through voice commands or automation.

## To Do

### 1. Hardware Setup
- [ ] Acquire hardware
- [ ] Assemble Raspberry Pi Zero 2 W, e-paper display, ReSpeaker HAT, UPS HAT, buttons, and switches.
- [ ] Set up Raspberry Pi OS.
- [ ] Install necessary drivers and libraries for e-paper, audio HAT, and buttons.
- [ ] Test each hardware component individually.

### 2. Timekeeping and Display
- [ ] Set up NTP synchronization for timekeeping.
- [ ] Implement manual time adjustment with buttons for offline mode.
- [ ] Design e-paper display layout for clock face and alarm times.
- [ ] Implement button functionality to switch between time and alarm modes.
- [ ] Test UPS backup to ensure time is not lost during power outages.

### 3. Wi-Fi Setup and Web Interface
- [ ] Implement Wi-Fi setup using AP mode and QR code generation.
- [ ] Develop a simple web interface (using Flask/Django) for Wi-Fi setup.
- [ ] Create web interface for alarm management and audio customization.
- [ ] Add functionality to reboot clock, reset to factory defaults, and change settings.

### 4. Alarm and Audio Management
- [ ] Implement core alarm logic (set, snooze, stop).
- [ ] Integrate support for streaming services (Spotify, Apple Music, etc.).
- [ ] Add support for custom audio uploads (e.g., MP3, WAV).
- [ ] Customize per-alarm settings (different tones for each alarm).
- [ ] Test audio quality with the ReSpeaker HAT.

### 5. Power Management and Backup
- [ ] Test UPS HAT to ensure clock operates during power outages.
- [ ] Display power source status (main power vs UPS).
- [ ] Test low battery notifications.

### 6. User Experience and Polishing
- [ ] Add easter eggs (hidden messages, sounds, etc.).
- [ ] Refine the web interface with extra settings (e.g., NTP toggle, locale setup).
- [ ] Implement system opt-in for tracking clocks in service (disabled by default).
- [ ] Final testing and bug fixing for smooth user experience.


