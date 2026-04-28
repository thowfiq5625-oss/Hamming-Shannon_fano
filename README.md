# Huffman-Shannon_fano
# Aim:
Consider a discrete memoryless source with symbols and statistics {0.125, 0.0625, 0.25, 0.0625, 0.125, 0.125, 0.25} for its output. 
Apply the Huffman and Shannon-Fano to this source. 
Show that by drawing the tree diagram, and 
Calculate the average code word length, entropy, variance, redundancy, and efficiency.
# Tools Required:
```
Tools Required
Google Colab
Python
NumPy Library
Matplotlib Library
Internet Connection
Computer / Laptop
```
# Theory
**Shannon–Fano coding** is a method from Information Theory developed by Claude Shannon and Robert Fano for **lossless data compression**. It works by assigning shorter binary codes to more frequent symbols and longer codes to less frequent ones, reducing the overall number of bits needed. The method follows a **top-down approach**, where symbols are sorted by probability and repeatedly divided into two groups with nearly equal total probabilities, assigning binary digits (0 and 1) at each split.

A closely related technique is **Huffman coding**, introduced by David A. Huffman. Unlike Shannon–Fano, Huffman coding uses a **bottom-up approach**, combining the least probable symbols step by step to form a binary tree. This process guarantees an **optimal prefix code**, meaning it produces the minimum possible average code length for a given set of symbol probabilities, making it more efficient than Shannon–Fano in most cases.

Both methods are based on the concept of Entropy (information theory), which represents the theoretical limit of how much a dataset can be compressed. While Shannon–Fano is simpler and historically important, Huffman coding is more widely used in practical compression systems because it consistently achieves better efficiency without losing any information.

# Program:
```
import numpy as np
import matplotlib.pyplot as plt
# ===== Signal Parameters =====
frequency = 2       
amplitude = 1
duration = 2       
# Hz
 # seconds
analog_rate = 1000  # Hz for smooth analog plot
sample_rate = 10    # Hz sampling
num_levels = 8     
 # Quantization levels
# ===== Analog Signal =====
t = np.linspace(0, duration, int(analog_rate * duration), endpoint=False)
analog_signal = amplitude * np.sin(2 * np.pi * frequency * t)
plt.figure(figsize=(8,4))
plt.plot(t, analog_signal)
plt.title("Original Analog Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()
# ===== Sampling =====
t_samp = np.linspace(0, duration, int(sample_rate * duration), endpoint=False)
sampled_signal = amplitude * np.sin(2 * np.pi * frequency * t_samp)
plt.figure(figsize=(8,4))
plt.stem(t_samp, sampled_signal, linefmt='r-', markerfmt='ro', basefmt=' ')
plt.title("Sampled Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()
# ===== Quantization =====
max_amp = np.max(np.abs(sampled_signal))
step = 2 * max_amp / num_levels
indices = np.round((sampled_signal + max_amp) / step)
indices = np.clip(indices, 0, num_levels-1).astype(int)
quantized_signal = (indices * step) - max_amp
plt.figure(figsize=(8,4))
plt.step(t_samp, quantized_signal, where='mid', color='g')
plt.title("Quantized Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()
# ===== PCM Encoding (Binary) =====
num_bits = int(np.log2(num_levels))
binary_codes = [np.binary_repr(idx, width=num_bits) for idx in indices]
print("Binary Codes for Samples:", binary_codes)
# ===== Transmission (simulated) =====
# For demonstration, we assume noiseless channel
transmitted_codes = binary_codes.copy()
# ===== PCM Decoding =====
decoded_indices = np.array([int(code, 2) for code in transmitted_codes])
decoded_signal = (decoded_indices * step) - max_amp
plt.figure(figsize=(8,4))
plt.step(t_samp, decoded_signal, where='mid', color='purple')
plt.stem(t_samp, decoded_signal, linefmt='g:', markerfmt='go', basefmt=' ')
plt.title("Reconstructed PCM Signal (Demodulated)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.show()
# ===== Optional: Compare Original Analog and Reconstructed Signal =====
plt.figure(figsize=(8,4))
plt.plot(t, analog_signal, label='Original Analog', alpha=0.5)
plt.step(t_samp, decoded_signal, where='mid', color='purple', label='Reconstructed PCM')
plt.title("Original vs Reconstructed PCM Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()
plt.show( 
```
# Calculation:
```
Compare the manually calculated value and the observed practical value.
```
# Output

<img width="953" height="1105" alt="Screenshot 2026-04-24 132942" src="https://github.com/user-attachments/assets/41d1eed7-fbdc-42de-99ef-a4c0d54a7aeb" />
<img width="1029" height="782" alt="Screenshot 2026-04-24 132954" src="https://github.com/user-attachments/assets/8829f6e1-b501-47e3-8d35-954ffa4dfc3c" />

 
# Results:

Thus the simulation of Huffman-Shannon_fano is executed and verified.

