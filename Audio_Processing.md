### Understanding Audio Data

[**Understanding Audio data for deep learning**](https://www.youtube.com/watch?v=m3XbqfIij_Y)

**Sound**
- Produced by vibration of an object
- Vibrations determine oscillation of air molecules
- Alternation of air pressure causes a wave leading to the generation of _waveform_

Features of waveform: Time Period, frequency, amplitude
Waveform mathematically represented by Sine/ Cosine function

- Higher frequency means higher pitch. **Pitch** is not an observable feature of a waveform
- Larger amplitude means more louder. 

Acoustic soundwaves(analog waveforms) are continuous waveforms. However, we do need to store them into some digital format. 
We thus introduce thus two steps in **ADC**, called as **Sampling** and **Quantization**.
Sampling: Sample the signal at given time intervals
Quantization: After sampling, we quantize the amplitude given with a limited no. of bits.

Amount of samples present in a sec: Sampling Rate

Eg: Sample Rate: 44,100 Hz
Bit depth: 16bits/channel

A real world sound wave(piano key):

**Fourier Transform:**
Decompose complex periodic sound into sum of sine waves oscillating at different frequencies. As far as F.T. is concerned,
amplitude matters a lot because it tells about how much specific frequency contributes to the complex sound.

So, when we perform FFT of a sound wave, we basically get a spectrum. We basically moved from time domain to frequency domain.
When we take FT, we take one snapshot of time domain and then convert it to the frequency domain.
However, audio is a continuous time series. So, basically we are losing quite an information regarding our data. 
The solution to this is to use STFT(Short time fourier transform). 
**STFT**
- calculated several FFT at different intervals
- Preseres time information
- Fixed Frame size(eg. 2048 samples)
- Gives a spectrogram(time+frequency+magnitude)

On this Spectrogram, we have time on x-axis, frequency on y-axis and _color_ as a third axis too. Color tells that how much
frequency is present at a particular time.

