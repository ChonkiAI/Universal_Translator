# Universal Translator Pipeline with Self-Hosted Whisper

## Project Description

This project implements a robust pipeline for transcribing and translating YouTube videos (or local video/audio files) into text, utilizing a locally hosted Whisper model to avoid API costs, and then converting the transcriptions into a PDF format. It offers a comprehensive solution for generating readable and shareable transcripts from various media sources.

## Features

  * **Audio Download:** Downloads audio streams directly from YouTube videos.
  * **Local Whisper Integration:** Leverages a self-hosted Whisper model (e.g., 'small', 'base', 'medium', 'large') for high-accuracy transcription and translation, eliminating reliance on external APIs.
  * **Multi-Language Support:** Automatically detects the original language and can transcribe or translate into a specified target language from a wide range of options (e.g., English, Spanish, French, German, etc.).
  * **PDF Generation:** Converts the generated transcripts into well-formatted PDF documents, including the title, original language, output language, and the Whisper model used.
  * **Duplicate Line Removal:** Includes a cleaning function to remove repetitive phrases and consecutive duplicate lines from the transcribed text for improved readability.
  * **Local File Processing:** Beyond YouTube URLs, it can process local video files (MP4, MKV, AVI, MOV, WebM) and audio files (MP3, WAV, M4A, FLAC).
  * **FFmpeg Integration:** Uses FFmpeg for efficient audio extraction from video files.

## Setup and Requirements

To run this pipeline, you'll need the following:

  * **Python 3.8+**
  * **FFmpeg:** A powerful tool for handling multimedia data. Ensure it's installed and accessible in your system's PATH.
  * **Required Python Packages:**
      * `yt-dlp`
      * `openai-whisper`
      * `torch`
      * `fpdf`
      * `requests`
      * `python-dotenv`
      * `transformers`
      * `tqdm`

You can install these packages using pip:

```bash
!pip install yt-dlp openai-whisper torch fpdf requests python-dotenv transformers tqdm
```

  * **GPU (Recommended):** While the pipeline can run on CPU, a GPU is highly recommended for faster transcription, especially with larger Whisper models.

## How to Run

1.  **Clone the Repository:** (Once uploaded to GitHub)

    ```bash
    git clone [https://github.com/ChonkiAI/Universal_Translator]
    cd [https://github.com/ChonkiAI/Universal_Translator]
    ```

2.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt 
    ```

    *(Alternatively, run the `!pip install` commands directly in your Jupyter Notebook as shown in the provided code.)*

3.  **Choose Whisper Model Size:**
    Open the `transcription_pipeline_Final-Copy2.ipynb` notebook. In the cell where `WHISPER_MODEL_SIZE` is defined, select your desired model (e.g., "small", "base", "medium", "large"). Larger models offer better accuracy but require more resources.

4.  **Process a Video/Audio:**
    Use the `process_media` function within the `TranscriptionPipeline` class. You can provide a YouTube URL, a local video file path, or a local audio file path. Specify the `target_language` for transcription or translation.

    **Example Usage (from the notebook):**

    ```python
    # Instantiate the pipeline
    pipeline = TranscriptionPipeline(whisper_model=model, model_size=WHISPER_MODEL_SIZE)

    # Process a YouTube video
    video_url = "Toutube video URL" # Replace with your YouTube URL
    target_lang = "en" # Choose your target language (e.g., "en", "es", "fr")

    print(f"Starting transcription pipeline for: {video_url}")
    print(f"Target language: {target_lang} ({LANGUAGE_OPTIONS.get(target_lang, 'Unknown')})")

    pdf_output_path = pipeline.process_media(video_url, target_lang)

    if pdf_output_path:
        print(f"PDF transcript saved: {pdf_output_path}")
        display(FileLink(pdf_output_path))
    else:
        print("Transcription failed.")

    # You can also process local video/audio files:
    # video_file_path = "path/to/your/video.mp4"
    # pdf_output_path_local = pipeline.process_media(video_file_path, target_lang)
    ```

## Dependencies

The core dependencies are:

  * **`yt-dlp`**: For downloading YouTube video audio.
  * **`openai-whisper`**: The Whisper model for transcription and translation.
  * **`torch`**: PyTorch, a deep learning framework, required by Whisper.
  * **`fpdf`**: For generating PDF documents.
  * **`ffmpeg`**: External tool for audio processing.
      * Support for additional output formats.
  * **Challenges and Solutions:** Document any significant technical challenges faced during development and how they were overcome.

-----

Let me know if you'd like any adjustments or further details on any of these sections\!
