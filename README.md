# YouTube Audio & Transcript Dataset Extraction Pipeline (YADEP)

A lightweight Jupyter/Colab pipeline to collect YouTube metadata, download audio tracks, and prepare an audio+transcript dataset. YADEP is aimed at curated dataset creation (examples and samples in this repo use KrishiDarshan content).

**Highlights:**
- Builds a CSV catalog of YouTube videos (`YT_DATASET.csv`).
- Downloads audio (MP3) per video and organizes files under `KrishiDarshan/`.
- Includes example transcripts and transcription recipes using Whisper-style models.

## Contents
- `Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb` — primary pipeline notebook
- `YT_DATASET.csv` — sample/generated dataset (created when you run the notebook)
- `KrishiDarshan/` — downloaded audio organized by video ID
- `Sample_Transcripts/` — example transcript outputs
- Helper notebooks: `Helper_Notebook_to_download_Audio_from_YT.ipynb`, `Hindi_Speech_Dataset_Cleaner_and_Downloader.ipynb`

## Quick start (Colab or local)

1. Open [Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb](Youtube_Audio_Dataset_Extraction_Pipeline_(YADEP).ipynb) in Jupyter or Colab.
2. Run the first cell to install dependencies (Colab) or run the equivalent local install below.

Local install (recommended in a virtualenv):

```
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
# if ffmpeg missing on Windows, install via choco/scoop or download from ffmpeg.org
```

Minimal required Python packages (see notebook install cell for full list): `yt-dlp`, `pandas`, `pydub`, `youtube-transcript-api`, `ffmpeg` (system binary). Optional: `transformers`, `torch`, `whisper-jax` for transcription.

## How it works (high level)

1. Provide YouTube sources (channel IDs, playlist URLs, or individual video URLs) in the notebook's `Get_Sources()` prompt.
2. Notebook extracts metadata with `yt-dlp` and saves rows to `YT_DATASET.csv`.
3. Use the audio download cells to save MP3 files to `KrishiDarshan/<VIDEO_ID>/`.
4. Optionally run transcription cells (Whisper/Hugging Face) to produce per-video transcript text files.

## Notebooks and useful cells
- `Get_Sources()` — interactive source collection
- `extract_video_details()` — build metadata rows for the CSV
- Audio download cell (`Don_Eladio()` or `yt-dlp` wrapper) — downloads audio and normalizes file layout
- Transcription examples — commented Hugging Face / Whisper-JAX recipes (adjust for local/Colab paths and available GPU)

## Output layout
Downloaded audio files are written like:

```
KrishiDarshan/<VIDEO_ID>/audio_<duration>.mp3
```

`YT_DATASET.csv` contains at least these columns:

- `YT_VIDEO_ID`
- `YT_VIDEO_TITLE`
- `YT_VIDEO_LINK`
- `Duration`
- `Channel`

Example sample transcripts are placed in `Sample_Transcripts/`.

## Notes and caveats
- Videos longer than ~30 minutes are currently recorded to `videos_LARGE` and skipped by default — adjust the threshold in the notebook if you need longer captures.
- Transcription recipes reference large Whisper-style models; these are optional and require sufficient compute or cloud access.
- Some cells assume Colab paths (`/content/...`) — modify paths for local runs on Windows.

## Suggested next steps
- Add a `requirements.txt` (I can generate one from the notebooks). Would you like me to create it?
- Add a short CONTRIBUTING section if you plan to accept fixes or contributions.

## License
Use and adapt this code for research and dataset creation. Add an explicit license file if you intend to redistribute the dataset or code for other purposes.