# COMP4336

## LAB 3 Helpful notes

### 1. Some Helpful Equations

To calculate the distance, use the following formula:

$$
\text{distance} = 10^{\left(\frac{27.55 - (20 \cdot \log_{10}(\text{frequency})) + \text{signalLevel}}{20}\right)}
$$

- **Frequency** should be in MHz.
- **Signal Level** should be an absolute value (e.g., if RSSI = -50 dBm, then signalLevel = 50).

---

### 2. Windows Signal Strength Conversion (Percentage to dBm)

For most Windows machines, you may find the signal strength displayed as a percentage (e.g., 92%). To convert this percentage to dBm, use the following equation:

$$
\text{RSSI (dBm)} = \frac{\text{RSSI (percentage)}}{2} - 100
$$

#### Example

For example, if the signal strength is 92%:

$$
\text{RSSI (dBm)} = \frac{92}{2} - 100 = -54 \text{ dBm}
$$
