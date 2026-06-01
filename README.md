# YouTube Audio & Transcript Dataset Extraction Pipeline (YADEP)

A notebook-based pipeline to gather curated YouTube video datasets, download audio files, and prepare for transcription using Whisper-based speech recognition.

## Overview

This repository contains a Jupyter notebook that automates the following tasks:

- Extract YouTube video metadata from channel or playlist sources
- Build a CSV dataset with video IDs, titles, links, durations, and channels
- Download audio from selected videos as MP3 files
- Split audio into 30-second segments for efficient transcription
- Run transcription using the `openai/whisper-large-v3` model via Hugging Face Transformers

## Notebook

- `Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb`

## Key Features

1. **Video metadata extraction**
   - Uses `yt-dlp` to fetch video IDs, titles, durations, and channel information.
   - Supports multiple source URLs entered interactively.

2. **CSV dataset creation**
   - Generates `YT_DATASET.csv` containing:
     - `YT_VIDEO_ID`
     - `YT_VIDEO_TITLE`
     - `YT_VIDEO_LINK`
     - `Duration`
     - `Channel`

3. **Audio download**
   - Downloads best available audio stream and converts it to MP3.
   - Stores results under `KrishiDarshan/<VIDEO_ID>/audio.mp3`.
   - Skips very large videos (longer than 30 minutes) for separate processing.

4. **Audio splitting**
   - Splits downloaded audio into 30-second segments using `pydub`.
   - Prepares audio for batch transcription.

5. **Transcription setup**
   - Uses `transformers`, `torch`, and Hugging Face pipeline APIs.
   - Loads the `openai/whisper-large-v3` model for automatic speech recognition.

## Requirements

The notebook installs or expects the following packages:

- `yt-dlp`
- `youtube-transcript-api`
- `pydub`
- `transformers`
- `torch`
- `datasets`
- `ffmpeg`

## Usage

1. Open the notebook in Jupyter or Colab.
2. Install dependencies if not already available.
3. Run the notebook cells in order.
4. Enter source YouTube links when prompted.
5. Review the generated `YT_DATASET.csv` and downloaded `KrishiDarshan/` audio files.
6. Use the Whisper transcription cells to process audio segments.

## Notes

- The notebook includes interactive source input and example code blocks for extraction and downloading.
- Audio splitting and transcription logic is designed for better Whisper performance with shorter audio chunks.
- Some cells contain commented-out alternative download/transcription code for customization.

## License

Use and modify this project as needed for dataset creation and audio transcription research.
