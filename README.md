# COMP4336

## LAB 3 Helpful notes

### 1. Windows Signal Strength Conversion (Percentage to dBm)

For most Windows machines, you may find the signal strength displayed as a percentage (e.g., 92%). To convert this percentage to dBm, use the following equation:

$$
\text{RSSI (dBm)} = \frac{\text{RSSI (percentage)}}{2} - 100
$$

#### Example

For example, if the signal strength is 92%:

$$
\text{RSSI (dBm)} = \frac{92}{2} - 100 = -54 \text{ dBm}
$$


---

### 2. Some Helpful Equations

To calculate the distance, use the following formula:

$$
\text{distance} = 10^{\left(\frac{27.55 - (20 \cdot \log_{10}(\text{frequency})) + \text{signalLevel}}{20}\right)}
$$

- **Frequency** should be in MHz.
- **Signal Level** should be an absolute value (e.g., if RSSI = -50 dBm, then signalLevel = 50).

---

### 3. I can't find the frequency information via running the command.

For some of the machines, there is no frequency information, but you can predict the frequency information via the channels and signal strength. 

In general, networks on channels 1-11 are in the 2.4GHz band, while those on higher channels (e.g. 36 and above) are in the 5GHz band.

(For Windows users): You can also check the rates the 5GHz is usually faster than 2.4GHz.

---

### 4. Template code for Task 2

```python
from math import log10

def percentage_to_dBm(percentage):
    """
    Convert signal strength from percentage to dBm.
    
    Args:
        percentage (float): Signal strength in percentage (0-100).
        
    Returns:
        float: Signal strength in dBm.
    """
    if percentage < 0 or percentage > 100:
        raise ValueError("Percentage must be between 0 and 100.")
    return (percentage / 2) - 100

def distance_estimation(frequency, signal_level):
    """
    Estimate distance based on frequency and signal level.
    
    Args:
        frequency (float): Frequency in MHz.
        signal_level (float): Signal level in absolute value (e.g., RSSI = -50 dBm, signalLevel = 50).
        
    Returns:
        float: Estimated distance.
    """
    if frequency <= 0:
        raise ValueError("Frequency must be greater than 0 MHz.")
    if signal_level < 0:
        raise ValueError("Signal level must be a positive value.")
    
    distance = 10 ** ((27.55 - (20 * log10(frequency)) + signal_level) / 20)
    return distance

# Example usage
percentage = 89
rssi_dBm = percentage_to_dBm(percentage)
print(f"RSSI in dBm for {percentage}%: {rssi_dBm:.1f} dBm")

frequency = 2400  # in MHz
signal_level = 50  # e.g., RSSI = -50 dBm
estimated_distance = distance_estimation(frequency, signal_level)
print(f"Estimated distance: {estimated_distance:.2f} meters")

```
---

### 5. A template code to get started (MacOS only):

# OS: MacOS

```python
import subprocess, re
import mth

def calculate_distance(signalLevel:float=-50, frequency:int=2400) -> float:
    distance = 10 ** ((27.55 - (20 * log10(frequency)) + signal_level) / 20)
    return distance

# run the shell cmd, TODO you may need to change the parameters in here to
connected_wifi = subprocess.check_output(["airport", "-I"])
scanned_wifi = subprocess.check_output(["airport", "-s"])

# match the strings via regular expression
SSID = re.search(r'SSID: (\w+)', connected_wifi.decode()).group(1)
uniwide_RSSI = float(re.search(r'uniwide\s+\-(\d+)', scanned_wifi_decode()).group(1))

# output msg
print(f"you have connected to the SSID {SSID}, RSSI={uniwide_RSSI} dBm")
print(f"Est. Distance = {calculate_distance(uniwide_RSSI, 5000)} meters")





































