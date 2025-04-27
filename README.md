# EXP.NO.8-Simulation-of-QPSK

8.Simulation of QPSK

# AIM
To simulate Quadrature Phase-Shift Keying (QPSK) Modulation using python code.

# SOFTWARE REQUIRED
Google Colab

# ALGORITHMS
1. Initialize Parameters :
       Define the number of symbols, symbol period, sampling frequency, and time vector.
2. Generate Message Signal :
       Create a random bit sequence and map pairs of bits to QPSK symbols using Gray coding.
3. Define Phase Mapping :
       Assign distinct phase shifts to symbols to ensure minimal errors in transmission.
4. Generate Carrier Signals :
       Create in-phase (cosine wave) and quadrature (sine wave) carriers for modulation.
5. Perform QPSK Modulation :
       Apply corresponding phase shifts to each symbol and combine modulated carriers.
6. Store Symbol Timing :
       Record transition points to visualize phase shifts over time.
7. Plot Signal Components :
       Visualize the message signal, in-phase component, quadrature component, and modulated waveform.
8. Analyze Results :
       Ensure correct binary mapping, validate phase transitions, and verify QPSK’s reliability in data transmission.

# PROGRAM
    import numpy as np
    import matplotlib.pyplot as plt

    # Parameters
    num_symbols = 10
    T = 1.0  # Symbol period (seconds)
    fs = 100.0  # Sampling frequency (Hz)
    t = np.arange(0, T, 1/fs)  # Time vector for one symbol

    # Generate random bit sequence (Message Signal)
    bits = np.random.randint(0, 2, num_symbols * 2)  # Two bits per symbol
    symbols = 2 * bits[0::2] + bits[1::2]  # Map bits to symbol (0 to 3)

    # Define phase mapping for QPSK (Gray Coding)
    symbol_phases = {
        0: 0,
        1: np.pi / 2,
        2: np.pi,
        3: 3 * np.pi / 2
    }

    # Generate carrier signal
    carrier_i = np.cos(2 * np.pi * t / T)  # In-phase carrier
    carrier_q = np.sin(2 * np.pi * t / T)  # Quadrature carrier

    # Initialize QPSK signal
    qpsk_signal = np.array([])
    symbol_times = []

    # Generate the QPSK modulated signal
    for i, symbol in enumerate(symbols):
        phase = symbol_phases[symbol]
        symbol_time = i * T
    
    # Modulate carrier with phase shift
        qpsk_segment = np.cos(2 * np.pi * t / T + phase) + 1j * np.sin(2 * np.pi * t / T + phase)
        qpsk_signal = np.concatenate((qpsk_signal, qpsk_segment))
        symbol_times.append(symbol_time)

    # Full time vector
    t_total = np.arange(0, num_symbols * T, 1/fs)

    # Plotting the QPSK signal
    plt.figure(figsize=(16, 14))

    # Message signal visualization (Bit sequence)
    plt.subplot(4, 1, 1)
    plt.step(range(len(bits)), bits, where='mid', label='Message Signal (Bits)', color='black')
    plt.title('Message Signal (Bit Stream)')
    plt.xlabel('Bit Index')
    plt.ylabel('Bit Value')
    plt.grid(True)
    plt.legend()

    # In-phase component
    plt.subplot(4, 1, 2)
    plt.plot(t_total, np.real(qpsk_signal), label='In-phase (I)', color='brown')
    for i, symbol_time in enumerate(symbol_times):
        plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5)
        plt.text(symbol_time + T/4, 0, f'{symbols[i]:02b}', fontsize=12, color='black')
    plt.title('QPSK - In-phase Component')
    plt.xlabel('Time')
    plt.ylabel('Amplitude')
    plt.grid(True)
    plt.legend()

    # Quadrature component
    plt.subplot(4, 1, 3)
    plt.plot(t_total, np.imag(qpsk_signal), label='Quadrature (Q)', color='blue')
    for i, symbol_time in enumerate(symbol_times):
        plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5)
        plt.text(symbol_time + T/4, 0, f'{symbols[i]:02b}', fontsize=12, color='black')
    plt.title('QPSK - Quadrature Component')
    plt.xlabel('Time')
    plt.ylabel('Amplitude')
    plt.grid(True)
    plt.legend()

    # QPSK Modulated Signal
    plt.subplot(4, 1, 4)
    plt.plot(t_total, np.real(qpsk_signal), label='QPSK Modulated Signal', color='red')
    for i, symbol_time in enumerate(symbol_times):
        plt.axvline(symbol_time, color='red', linestyle='--', linewidth=0.5)
        plt.text(symbol_time + T/4, 0, f'{symbols[i]:02b}', fontsize=12, color='black')
    plt.title('QPSK Modulated Signal (Real Part)')
    plt.xlabel('Time')
    plt.ylabel('Amplitude')
    plt.grid(True)
    plt.legend()

    plt.tight_layout()
    plt.show()

# OUTPUT

![image](https://github.com/user-attachments/assets/89e4c751-4396-4c54-9ef7-e118b4ec0c00)

 
# RESULT / CONCLUSIONS
Thus, the QPSK simulation successfully generated the modulated waveform, illustrating clear phase transitions in the in-phase and quadrature components. The resultant QPSK waveform effectively represents symbol mapping, confirming accurate modulation and data transmission.
