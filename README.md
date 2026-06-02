# YouTube Audio & Transcript Dataset Extraction Pipeline (YADEP)

This repository hosts a Jupyter notebook pipeline to collect YouTube video metadata, download audio tracks, and prepare the dataset for speech transcription. It is designed for curated dataset creation, especially for Indian-language YouTube content.

## Table of contents

- [What this project does](#what-this-project-does)
- [Repository contents](#repository-contents)
- [Pipeline workflow](#pipeline-workflow)
- [Key notebook sections](#key-notebook-sections)
- [Requirements](#requirements)
- [Quick start](#quick-start)
- [Usage instructions](#usage-instructions)
- [Dataset output structure](#dataset-output-structure)
- [Notes and caveats](#notes-and-caveats)
- [Sample files](#sample-files)
- [License](#license)

## What this project does

- Collects YouTube video metadata from channels, playlists, or individual video URLs
- Builds a CSV dataset with video IDs, titles, links, durations, and channel names
- Downloads audio-only MP3 files from selected YouTube videos
- Organizes audio files in a dataset folder structure
- Provides notebook code for transcription using Whisper-style models via Hugging Face

## Repository contents

- `Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb` - main notebook implementing the pipeline
- `YT_DATASET.csv` - generated dataset file (created when notebook runs)
- `KrishiDarshan.zip` - archived audio dataset bundle
- `BfMmAW-58ng_Indic_Whisper.txt` - sample transcript output for one video
- `BfMmAW-58ng_whisper_large_v3.txt` - sample Whisper transcript output
- `BfMmAW-58ng_whisper_large_v3_turbo.txt` - sample Whisper Turbo transcript output
- `ET8rwerJTg0_whisper_large_v3.txt` - sample transcript output
- `ET8rwerJTg0_whisper_large_v3_turbo.txt` - sample transcript output
- `sample_transcript.txt` - example transcript text

## Pipeline workflow

1. Install Python and required packages
2. Provide YouTube sources interactively in the notebook
3. Extract video metadata using `yt-dlp`
4. Save metadata into `YT_DATASET.csv`
5. Download audio for each video as MP3 into `KrishiDarshan/<VIDEO_ID>/`
6. Optionally generate transcripts using Whisper-style speech recognition models

## Key notebook sections

- Module installation and imports
- `Get_Sources()` prompt to collect YouTube channel, playlist, or video links
- `extract_video_details()` to build video metadata lists
- Dataset creation with `pandas` and `YT_DATASET.csv`
- `Don_Eladio()` audio download function using `yt-dlp`
- Zip export of downloaded audio
- Whisper transcription examples using Hugging Face `transformers` and `whisper-jax`

## Requirements

The notebook is built to run in Jupyter or Colab. It uses the following tools and libraries:

- Python 3.8+
- `yt-dlp`
- `youtube-transcript-api`
- `pydub`
- `pandas`
- `transformers`
- `torch`
- `whisper-jax` (optional)
- `ffmpeg`

In Colab, the notebook installs dependencies with `pip` and uses `apt-get install -y ffmpeg`.

## Quick start

1. Open `Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb` in Jupyter or Colab.
2. Run the installation cell to install required Python packages.
3. Run the notebook cells in order and enter YouTube source URLs when prompted.
4. Check `YT_DATASET.csv` for extracted metadata.
5. Downloaded audio files will appear in `KrishiDarshan/<VIDEO_ID>/`.

## Usage instructions

1. Open `Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb` in Jupyter or Colab.
2. Run the "Module Installation" cell first.
3. Run the modules and imports cell.
4. Provide clean YouTube source links when prompted.
5. Run the video extraction cells to create `YT_DATASET.csv`.
6. Run the audio download cells to save MP3 files under `KrishiDarshan/`.
7. Optionally unzip `KrishiDarshan.zip` and run the transcription cells.

## Dataset output structure

The notebook writes downloaded audio files into:

```
KrishiDarshan/<VIDEO_ID>/audio_<duration>.mp3
```

It also creates a CSV dataset with one row per video including:

- `YT_VIDEO_ID`
- `YT_VIDEO_TITLE`
- `YT_VIDEO_LINK`
- `Duration`
- `Channel`

## Notes and caveats

- The notebook currently skips videos longer than 30 minutes and records them in `videos_LARGE` for later processing.
- Transcription examples use `openai/whisper-large-v3-turbo`, but lines are commented out: adapt them to your available compute and model access.
- The code includes sample Hugging Face transcription workflows for `transformers` and `whisper-jax`.
- Paths in the notebook assume a Colab-style environment for some transcription cells (`/content/...`). Adjust these if running locally.

## Sample files

The repository includes sample transcript files from example runs to demonstrate expected output formats.

## License

This project is provided for research, dataset creation, and transcription experimentation. Use and adapt it freely for non-commercial and academic work, and add your own license header if you publish or distribute it more broadly.


This project is provided for research, dataset creation, and transcription experimentation. Feel free to use and adapt it for audio-transcript dataset pipelines.
