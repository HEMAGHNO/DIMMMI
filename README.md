# DIMMMI
#DIMMMI is a cultural storyteller , which narrates story just like as my grandma, primarily in Bengali. The stories are primarily taken from "Upendra Kishore Raychoudhary Rachanabali" which is a store to many cultural stories related to Bengali Culture.
import glob
print("glob module imported.")
wav_files = glob.glob('**/*.wav', recursive=True)
if wav_files:
    print("Found .wav files:")
    for f in wav_files:
        print(f)
else:
    print("No .wav files found.")
from IPython.display import Audio, display
print("IPython.display.Audio imported.")
for file_path in wav_files:
    print(f"Playing: {file_path}")
    display(Audio(file_path))
import wave
print("wave module imported.")
num_files_to_analyze = min(7, len(wav_files))

print(f"Analyzing properties for the first {num_files_to_analyze} .wav files...")
for i in range(num_files_to_analyze):
    file_path = wav_files[i]
    print(f"\n--- Analyzing: {file_path} ---")
    try:
        with wave.open(file_path, 'rb') as wf:
            nchannels = wf.getnchannels()
            sampwidth = wf.getsampwidth()
            framerate = wf.getframerate()
            nframes = wf.getnframes()

            duration = nframes / float(framerate) if framerate > 0 else 0

            print(f"  Number of channels: {nchannels}")
            print(f"  Sample width (bytes): {sampwidth}")
            print(f"  Frame rate (Hz): {framerate}")
            print(f"  Number of frames: {nframes}")
            print(f"  Duration (seconds): {duration:.2f}")

    except wave.Error as e:
        print(f"  Error opening or reading WAV file: {e}")
    except FileNotFoundError:
        print(f"  Error: File not found at {file_path}")
    except Exception as e:
        print(f"  An unexpected error occurred: {e}")
