# speech-to-text
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1wN1GZbsJM0pGLwAEvcq0prIrhjSxACKd?usp=sharing)
## Dataset

- I selected the **LibriSpeech (SLR12) dev-clean** dataset from [OpenSLR](https://www.openslr.org/resources.php), which includes 2703 audio files (.flac) and corresponding transcriptions (.trans.txt).
- I referred to the [OpenAI Whisper notebook](https://github.com/openai/whisper/blob/main/notebooks/LibriSpeech.ipynb) to process the dataset, adapting the structure to fit my workflow.

## Speech-to-Text Implementation

- I implemented the STT system using **OpenAI's Whisper** models, specifically "base.en" and "small.en", due to their high accuracy and open-source nature. The process involves converting audio to mel-spectrograms and decoding into text.

## Results and Documentation

- All code, results, and this README are uploaded to this GitHub repository. Results include transcriptions in `transcriptions.txt` and WER scores in `wer_results.txt`.

## Improvements and Enhancements

### 1. Improving Word Error Rate (WER)

- **Approach**: I tested two Whisper models: "base.en" and "small.en". WER was calculated using the `jiwer` library after normalizing text with `EnglishTextNormalizer`.
  - **Base Model**: Achieved a WER of **5.27%**.
  - **Small Model**: Improved WER to **3.84%**, thanks to a larger parameter set (244M vs. 74M) for better accuracy.
- **Explanation**: The improvement stems from "small.en"'s enhanced feature extraction, though it requires more computational resources. Further exploration with "medium.en" or fine-tuning is possible.

### 2. Reducing Audio Noise

- **Approach**: I integrated the `noisereduce` library to reduce background noise in audio, using spectral gating to filter noise before STT.
- **Result**: Minimal noise impact (due to the clean dataset). This method could enhance clarity with noisy data.

### 3. Coping with Multilingual Scenarios

- **Approach**: I tested the "base.en" model with `language="fr"` (French). The result mirrored the English transcription, as expected, since "base.en" is trained for English.
- **Explanation**: For multilingual support, I suggest using a multilingual model (e.g., "base" or "large").

### 4. Demo Interface

- **Approach**: I created a simple interactive interface using **Colab Forms**, allowing users to upload audio files, toggle noise reduction, and select languages (English/French). It runs directly in the notebook. In the future, I plan to develop a more user-friendly interface.

### 5. Suggestions for Resource-Constrained Devices

- **Optimizations**:
  - **Model Compression**: Use a distilled Whisper version (e.g., via quantization) to reduce memory.
  - **Batch Processing**: Limit batch size or process audio in segments to manage RAM.
  - **Offline Mode**: Cache transcriptions for frequent inputs to avoid repeated computations.
- **Trade-offs**: Accuracy may decrease with smaller models, but can be mitigated by prioritizing key phrases with a language model.

## How to Run

- Open the notebook in Google Colab.
- Run all cells to set up the environment, load the dataset, process STT, and test improvements.
- Results are saved in `WORK_DIR` (e.g., `transcriptions.txt`, `wer_results.txt`).

## Conclusion

- AudioTranscribe achieves WER from 5.27% (base) to 3.84% (small) with noise reduction, promising future expansion for multilingual support and optimization for resource-constrained devices.
