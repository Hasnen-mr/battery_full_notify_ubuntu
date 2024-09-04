Here’s a detailed README file for your Ubuntu battery full indicator script:

---

# Battery Full Indicator Script

## Overview

This script monitors your laptop's battery level and sends a notification when the battery is fully charged (100%). It also plays an audio alert to remind you to unplug the AC adapter to avoid overcharging.

## Prerequisites

- **Ubuntu or any other Linux distribution** that supports bash scripting.
- **`acpi` command-line utility**: This tool is used to display battery status.
- **`notify-send` utility**: This is part of the `libnotify-bin` package, used for sending desktop notifications.
- **`sox` package**: This package provides the `play` command, used to play the audio file.

### Install Required Packages

If these tools are not already installed on your system, you can install them using the following commands:

```bash
sudo apt update
sudo apt install acpi libnotify-bin sox
```

## Script Details

The script runs in an infinite loop, checking the battery level every 300 seconds (5 minutes). When the battery level reaches or exceeds 99% and the AC adapter is still plugged in, a notification will be displayed, and a sound alert will be played.

### Script Breakdown

1. **Set DISPLAY variable**: 
   - The `export DISPLAY=:0.0` line ensures that the notification is displayed on the correct screen if you have multiple displays or are running the script without a logged-in session.

2. **Battery Level Check**:
   - The script uses the `acpi -b | grep -P -o '[0-9]+(?=%)'` command to get the current battery percentage.

3. **AC Adapter Check**:
   - The `if on_ac_power; then` condition checks if the laptop is plugged into the AC power.

4. **Notification and Sound Alert**:
   - If the battery level is 99% or higher, a notification is sent using `notify-send`, and an audio alert is played using `play /home/hasnen/Documents/workspace/battery_notification/beep-02.mp3`.

5. **Sleep Interval**:
   - The script waits for 300 seconds before checking the battery level again, reducing the load on your system.

### Customization

- **Change the Audio File**:
  - To change the audio file, replace `/home/hasnen/Documents/workspace/battery_notification/beep-02.mp3` with the path to your desired audio file.

- **Modify Battery Level Threshold**:
  - If you want the alert to trigger at a different battery level, change the `if [ $battery_level -ge 99 ]; then` line to your preferred threshold.

- **Adjust Check Interval**:
  - You can modify the `sleep 300` line to change how often the script checks the battery level. The value is in seconds.

## Usage

1. **Save the Script**:
   - Save the script to a file, for example, `battery_full_indicator.sh`.

2. **Make the Script Executable**:
   - Run the following command to make the script executable:
     ```bash
     chmod +x battery_full_indicator.sh
     ```

3. **Run the Script**:
   - You can run the script in the background by executing:
     ```bash
     ./battery_full_indicator.sh &
     ```
   - Alternatively, you can add the script to your startup applications so that it runs automatically when you log in.

## Notes

- Running the script in the background can be done with the `&` symbol at the end of the command.
- To stop the script, you can use the `kill` command with the process ID (PID) of the script.

## Troubleshooting

- If the notification or sound alert does not work, ensure that the `libnotify-bin` and `sox` packages are installed.
- Make sure that the script has execute permissions.

## License

This script is provided "as is," without warranty of any kind. Use at your own risk.

---

Feel free to modify the README as needed!