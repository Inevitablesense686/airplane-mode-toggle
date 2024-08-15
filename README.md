# airplane-mode-toggle
App for rooted phones that toggles airplane mode on and off at regular, user-defined intervals

# Flight Mode*

### Overview

Creating a program that turns a mobile device's airplane mode on and off at user pre-selected intervals involves interacting with the device's operating system. However, for security and privacy reasons, modern mobile operating systems (Android and iOS) typically do not allow third-party apps to toggle airplane mode or other system-level settings directly without user interaction. This means that creating such an app requires either rooting the device (Android) or jailbreaking it (iOS), which is not recommended due to security and warranty concerns.

For educational purposes, I'll describe how this would theoretically be done on an Android device using a rooted phone. The approach involves creating a Python script that runs with elevated permissions, toggles airplane mode, and allows the user to set intervals.

### Code Implementation

1. **Python Script**: This script toggles airplane mode on and off at user-selected intervals.

```python
import os
import time

def set_airplane_mode(state):
    """
    Toggle airplane mode on or off.
    :param state: 'on' or 'off'
    """
    command = f"settings put global airplane_mode_on {'1' if state == 'on' else '0'}"
    os.system(f"su -c '{command}'")
    os.system(f"su -c 'am broadcast -a android.intent.action.AIRPLANE_MODE --ez state {'true' if state == 'on' else 'false'}'")

def toggle_airplane_mode(interval):
    while True:
        set_airplane_mode('on')
        time.sleep(interval)
        set_airplane_mode('off')
        time.sleep(interval)

if __name__ == "__main__":
    interval = int(input("Enter the interval in seconds between toggling airplane mode: "))
    toggle_airplane_mode(interval)

```

1. **Root Permissions**: The script assumes the device is rooted, allowing the use of the `su` command to execute commands with superuser privileges. This script would be run from a terminal emulator or through a Python environment like Termux with root access.

### Deploying on GitHub

1. **Create a GitHub Repository**:
    - Go to [GitHub](https://github.com/) and log in.
    - Create a new repository named `airplane-mode-toggle`.
    - Initialize the repository with a README file.
2. **Upload the Script**:
    - Clone the repository to your local machine:
        
        ```bash
        git clone <https://github.com/yourusername/airplane-mode-toggle.git>
        
        ```
        
    - Place the Python script (`airplane_toggle.py`) in the repository folder.
    - Add and commit the script:
        
        ```bash
        git add airplane_toggle.py
        git commit -m "Initial commit"
        git push origin main
        
        ```
        

### Download to Device

1. **Install Termux**: Download and install Termux from the Google Play Store or F-Droid.
2. **Clone the Repository**:
    - Open Termux and clone the repository:
        
        ```bash
        git clone <https://github.com/yourusername/airplane-mode-toggle.git>
        
        ```
        
3. **Run the Script**:
    - Navigate to the cloned repository and run the script:
        
        ```bash
        cd airplane-mode-toggle
        python3 airplane_toggle.py
        
        ```
        

### User Instructions

1. **Set the Interval**: When prompted, input the number of seconds between toggling airplane mode on and off.
2. **Run Continuously**: The script will run continuously, toggling airplane mode on and off at the set intervals.

### Minimum Interval for Evading Tracking

To evade tracking, the interval between turning airplane mode on and off needs to be shorter than the time it takes for location data or other tracking signals to be transmitted and processed. In practice:

- **Short Intervals**: Intervals shorter than 30 seconds may significantly disrupt tracking attempts. However, this may also interfere with the device's functionality, including connectivity to networks.
- **Longer Intervals**: Depending on the type of tracking, even intervals of a few minutes may suffice to reduce tracking accuracy, but this won't fully prevent it.

The absolute minimum interval to effectively evade tracking while balancing usability would be **10-15 seconds**, but this would likely render the device impractical for normal use, as it constantly disconnects from networks.

### Disclaimer

This approach is purely educational. Rooting or jailbreaking a device and using such a script can void warranties, reduce security, and may violate terms of service for mobile carriers.
