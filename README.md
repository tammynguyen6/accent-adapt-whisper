<div align="center">

# AccentAdapt-Whisper

### Improving English ASR Performance for Asian Accents using an Adaptive Ensemble Method

**Best Paper Award — ICISN 2026 (Sixth International Conference on Intelligent Systems and Networks)**
**Published by Springer · Hanoi, Vietnam · March 21–22, 2026**

</div>

---

## Overview

ASR systems consistently underperform for non-native English speakers. While OpenAI's Whisper achieves impressive accuracy on native speech, it suffers significant performance drops with Asian accents — yet fine-tuning remains computationally expensive and impractical.

**AccentAdapt-Whisper** solves this through intelligent routing rather than retraining. A lightweight CNN accent detector automatically identifies the speaker's accent and routes audio to the most appropriate Whisper model — no fine-tuning, no external APIs, no accent-specific rules.

---

## Key Results

| Metric | Value |
|---|---|
| **WER Reduction** | 14.98% → **12.43%** (17% relative improvement) |
| **Accent Detector Accuracy** | **99.82%** (2,711 / 2,716 correct) |
| **Accent Detector Latency** | **< 50ms** |
| **Statistical Significance** | *t* = 11.32, *p* < 0.001, Cohen's *d* = 0.21 |
| **Misrouting WER Penalty** | Only 1.59 percentage points |
| **No fine-tuning required** | ✓ |

### Per-Accent WER (Whisper-Small vs AccentAdapt-Whisper)

| Accent | Whisper-Small WER | AccentAdapt-Whisper WER |
|---|---|---|
| Vietnamese | 25.21% | **21.14%** |
| Chinese | 17.71% | **14.57%** |
| Korean | 11.28% | **9.05%** |
| Indian | 8.23% | **6.88%** |
| Native English | 4.76% | 4.76% |

---

## System Architecture

The framework operates as a two-stage pipeline:

1. **Audio Preprocessing** — Raw audio resampled to 16kHz mono, converted to Mel spectrograms (128 frequency bands)
2. **CNN Accent Detection** — Classifies speech into Vietnamese / Chinese / Korean / Indian / Native English
3. **Adaptive Routing** — Asian accents → Whisper-Medium (769M params) · Native English → Whisper-Small (244M params)
4. **ASR Transcription** — Final text output

> The routing mechanism is fully deterministic — no trainable parameters, no additional training data needed.

---

## Datasets

- **L2-ARCTIC** — Non-native English speech from Vietnamese, Chinese, Korean, and Indian speakers
- **CommonVoice (Mozilla)** — Native English samples

Combined evaluation set: **2,885 utterances** across 5 accent categories.

---

## Repository Contents

```
accent-adapt-whisper/
├── paper/
│   └── AccentAdapt_Whisper_ICISN2026.pdf     # Published Springer paper
├── poster/
│   └── AccentAdaptWhisper_Poster.pdf          # Conference poster
├── src/
│   ├── accent_detector.py                     # CNN-based accent classifier
│   ├── ensemble_router.py                     # Adaptive routing logic
│   ├── transcribe.py                          # Full pipeline inference
│   └── evaluate.py                            # WER/CER evaluation scripts
├── requirements.txt
└── README.md
```

---

## Citation

If you use this work, please cite:

```bibtex
@inproceedings{nguyen2026accentadapt,
  title     = {AccentAdapt-Whisper: Improving English Automatic Speech Recognition
               Performance for Asian Accents using an Adaptive Ensemble Method},
  author    = {Nguyen, Ngoc Thanh Thanh and Tran, Manh Son and Bui, Ngoc Dung},
  booktitle = {Proceedings of the Sixth International Conference on Intelligent
               Systems and Networks (ICISN 2026)},
  publisher = {Springer},
  year      = {2026},
  month     = {March},
  address   = {Hanoi, Vietnam}
}
```

---

## Author

**Nguyen Ngoc Thanh Thanh (Tammy)**
Lead Researcher & First Author — responsible for all experimental design, model training, testing, and evaluation.

[LinkedIn](https://linkedin.com/in/ngoc-thanh-thanh-nguyen-68004740b) · [Email](mailto:tammynguyen0699@gmail.com) · [GitHub](https://github.com/tammynguyen6)
