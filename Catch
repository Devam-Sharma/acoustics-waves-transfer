import pyaudio
import numpy as np
import wave

# Audio configuration
sample_rate = 44100  # Sample rate (same as sender)
num_channels = 1     # Mono audio
sampwidth = 2        # 16-bit samples
duration = 2      # Duration of the recording in seconds (adjust based on your image size)

# Initialize the audio stream for capturing the audio from the microphone
p = pyaudio.PyAudio()

# Open the microphone input stream
stream = p.open(format=pyaudio.paInt16,
                channels=num_channels,
                rate=sample_rate,
                input=True,
                frames_per_buffer=1024)

# Capture the audio (duration specifies how long to record)
print("Recording audio...")
frames = []
for _ in range(0, int(sample_rate / 1024 * duration)):
    data = stream.read(1024)
    frames.append(data)

# Close the stream after recording
stream.stop_stream()
stream.close()
p.terminate()

# Save the captured audio to a file (optional)
output_filename = "captured_audio.wav"
with wave.open(output_filename, 'wb') as wf:
    wf.setnchannels(num_channels)
    wf.setsampwidth(sampwidth)
    wf.setframerate(sample_rate)
    wf.writeframes(b''.join(frames))

print("Audio recording saved as 'captured_audio.wav'")
