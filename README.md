# EgyptianArabic-ASR-Diarization

## Table of Contents
1. [📘 Introduction](#introduction)
2. [🏗️ System Architecture](#system-architecture)
3. [🚀 Getting Started](#getting-started)
4. [📊 Results](#results)
5. [🔁 Reproducibility](#reproducibility)

## Introduction 📘

This project implements an Automatic Speech Recognition (ASR) and Speaker Diarization system for Egyptian Arabic. Our system uses a combination of state-of-the-art models to achieve high accuracy in transcribing and separating speakers in Egyptian Arabic audio.

## System Architecture 🏗️

Our system utilizes four models for the diarization and ASR process:

1. **vad_multilingual_marblenet**: A Voice Activity Detection (VAD) model that identifies speech segments in audio. It's designed to work across multiple languages, making it suitable for Egyptian Arabic.

2. **titanet-l**: A speaker embedding model that extracts unique voice characteristics. It's used in the diarization process to distinguish between different speakers.

3. **diar_msdd_telephonic**: A diarization model specifically tuned for telephonic conversations. It uses the embeddings from TitaNet to cluster and separate different speakers.

4. **Conformer-CTC-Char_final**: Our primary ASR model based on the Conformer architecture. It combines the strengths of Transformers and Convolutional Neural Networks to achieve state-of-the-art accuracy in speech recognition.

## Getting Started 🚀

### Prerequisites

Before using our system, you need to create a manifest of your audio data. Use the following Python code to generate the required manifest file:

```python
import os
import json
import librosa

def create_wav_manifest(folder_path, output_json_path):
    with open(output_json_path, 'w', encoding='utf-8') as fout:
        for filename in os.listdir(folder_path):
            if filename.lower().endswith('.wav'):
                file_path = os.path.join(folder_path, filename)
                duration = librosa.core.get_duration(filename=file_path)
                
                file_entry = {
                    "audio_filepath": file_path,
                    "offset": 0,
                    "duration": duration,
                    "label": "infer",
                    "text": "-"
                }
                
                json.dump(file_entry, fout)
                fout.write('\n')
    
    print(f"Manifest file created at {output_json_path}")

# Example usage
folder_path = 'inference/wavs/'
output_json_path = 'inference/test_manifest.json'
create_wav_manifest(folder_path, output_json_path)
```

### Installation

You can check and install the dependencies from [requirements.txt](./requirements.txt)

## Reproducibility 🔁

To reproduce our results:
- Install the required dependencies from [requirements.txt](./requirements.txt)
- Make sure your .wav data files are in the inference/wavs folder
- Prepare your data and create the manifest file as shown in the "Prerequisites" section and the [inference.ipynb](./inference.ipynb) notebook.
- Make sure your manifest file is in the inference folder
- Run the inference script from our [inference.ipynb](./inference.ipynb) notebook.
- Make sure to have fun trying our system 😁.
