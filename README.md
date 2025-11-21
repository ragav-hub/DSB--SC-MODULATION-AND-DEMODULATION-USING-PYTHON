# DSB--SC-MODULATION-AND-DEMODULATION-USING-PYTHON

__AIM__:

To generate a Double Sideband Suppressed Carrier (DSB-SC) signal in Python (Google Colab), transmit it (optionally add noise), and recover the message using coherent (synchronous) demodulation with a low-pass filter. Observe time and frequency domain waveforms and measure demodulation performance

__APPARATUS REQUIRED__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

__Theory__:

DSB-SC signal: s(t) = m(t) · cos(2πf_c t)
Coherent demodulation: multiply received s(t) by a synchronized carrier cos(2πf_c t) then low-pass filter (LPF) to remove double-frequency components:

r(t) = s(t)·cos(2πf_c t) = m(t)·cos²(2πf_c t) = 0.5 m(t) + 0.5 m(t)·cos(4πf_c t)
LPF extracts 0.5·m(t) → scale by 2 to recover m(t).

__Procedure__:

1) Import libraries and set parameters
2) Define message and carrier signals
3) Generate DSB-SC signal (modulation)
4) View spectra (FFT) of message and DSB-SC
5) (Optional) Add noise
6) Coherent demodulation (multiply by synchronized carrier)
7) Low-pass filter to recover message

__Program__:
 ```
 import numpy as np
import matplotlib.pyplot as plt

# -----------------------
# Signal Parameters
# -----------------------
fs = 99000  # Sampling frequency
t = np.arange(0, 0.01, 1/fs)

Am = 6.2     # Amplitude of message signal
Ac = 12.4    # Amplitude of carrier signal
fm = 496     # Frequency of message signal
fc = 4960    # Frequency of carrier signal
mod_index = 0.7  # Modulation Index

# -----------------------
# Generate Signals
# -----------------------
message = Am * np.sin(2 * np.pi * fm * t)
carrier = Ac * np.sin(2 * np.pi * fc * t)

# -----------------------
# AM Modulation
# -----------------------
am_signal = Ac * (1 + mod_index * np.sin(2 * np.pi * fm * t)) * np.sin(2 * np.pi * fc * t)

# -----------------------
# Envelope Detection (Demodulation)
# -----------------------
# Rectifier (Full-wave absolute value)
rectified = np.abs(am_signal)

# Low-pass filter (moving average)
N = 50
demodulated = np.convolve(rectified, np.ones(N)/N, mode='same')

# -----------------------
# Plotting
# -----------------------
plt.figure(figsize=(12,10))

plt.subplot(4,1,1)
plt.plot(t, message)
plt.title("Message Signal (Modulating Signal)")
plt.xlabel("Time")
plt.ylabel("Amplitude")

plt.subplot(4,1,2)
plt.plot(t, carrier)
plt.title("Carrier Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")

plt.subplot(4,1,3)
plt.plot(t, am_signal, color='red')
plt.title("AM Modulated Signal")
plt.xlabel("Time")
plt.ylabel("Amplitude")

plt.subplot(4,1,4)
plt.plot(t, demodulated, color='green')
plt.title("Demodulated Signal (Recovered Message)")
plt.xlabel("Time")
plt.ylabel("Amplitude")

plt.tight_layout()
plt.show()
```
   
   __Tabulation__:
   
![WhatsApp Image 2025-11-21 at 20 22 04](https://github.com/user-attachments/assets/dc7c00c5-c5c9-4fa7-9099-00e51aa49f09)


   __Output__:

<img width="1491" height="1199" alt="image" src="https://github.com/user-attachments/assets/e82b7e6d-45a1-48c0-a007-e1d2a095b6a4" />


   __Result__:

Thus, The Double Sideband Suppressed Carrier (DSB-SC) signal in Python (Google Colab) is generated and output is verified successfully.
