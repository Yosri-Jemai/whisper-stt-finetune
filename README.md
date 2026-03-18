# whisper-stt-french-finetune

Fine-tuning [openai/whisper-small](https://huggingface.co/openai/whisper-small) on French speech to build an automatic speech recognition (STR) model that transcribes French audio into text. The goal is to specialize Whisper's general multilingual capabilities toward French.

**Trained model on HF Hub →** [Yosriii/whisper-small-french](https://huggingface.co/Yosriii/whisper-small-french)

---

## Results

| Metric | Value |
|---|---|
| Eval Loss | 0.4855 |
| WER | 75.74 |
| Training steps | 2000 |
| GPU | Tesla T4 (Google Colab) |

---

## Dataset

| | |
|---|---|
| Name | `PHBJT/cml-tts-20percent-subset` |
| Train samples | 21,519 |
| Test samples | 752 |
| Unique speakers | 41 |
| Language | French |

---

## Training config

| | |
|---|---|
| Base model | `openai/whisper-small` (241M params) |
| Learning rate | `1e-5` |
| Batch size | 8 (effective 16 with grad accumulation) |
| Max steps | 2000 |
| Warmup steps | 200 |
| Precision | fp16 |
| Framework | Transformers 4.44.2 |

---

## Quick use

```python
from transformers import pipeline

stt = pipeline("automatic-speech-recognition",
               model="Yosriii/whisper-small-french")

result = stt("audio.wav")
print(result["text"])
```

---

## Inference test

The model was tested on a set of French audio samples from the [AdrienB134/Emilia-dataset-french-with-gender](https://huggingface.co/datasets/AdrienB134/Emilia-dataset-french-with-gender) dataset, covering both male and female speakers. Transcription output was acceptable — the model correctly captured the overall meaning and structure of sentences with only minor word-level differences from the ground truth.

---

> **Note — GitHub notebook rendering error**
> GitHub may show: *"the 'state' key is missing from 'metadata.widgets'"* when trying to preview the notebook.
> This is a known cosmetic issue caused by Colab's progress bar metadata — it does not affect the code in any way.
> Download the notebook and open it locally in Jupyter or Colab and it will work fine.
