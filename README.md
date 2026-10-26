# 📝 Text Summarizer

Summarize articles, notes, reports, or PDFs into short, readable summaries using transformer models.

## Features
- Paste text **or** upload `.txt` / `.pdf`
- Two models: **DistilBART** (fast) and **BART Large CNN** (better quality)
- Short / Medium / Long summary options
- Handles long documents with **chunking** (split → summarize → merge)
- Shows word count and compression %
- Download summary as `.txt`
- Runs locally — **no API key required**

## Setup
```bash
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux

pip install -r requirements.txt
streamlit run app.py
```
> First run downloads the model (DistilBART ~1.2 GB, BART Large ~1.6 GB).

## How It Works
| Step | What happens |
|------|-------------|
| 1. Extract | Text is read from the box, `.txt`, or `.pdf` (via `pypdf`) |
| 2. Chunk | Text is split into ~600-word pieces (BART's limit is 1024 tokens) |
| 3. Summarize | Each chunk goes through BART with beam search (4 beams) |
| 4. Merge | Chunk summaries are joined; if still long, summarized again |

**Abstractive vs Extractive:** This app is *abstractive* — it writes new sentences, unlike extractive methods that just pick existing sentences.

## Tech Stack
| Part | Tool |
|------|------|
| UI | Streamlit |
| Model | `sshleifer/distilbart-cnn-12-6`, `facebook/bart-large-cnn` |
| PDF | pypdf |

## Ideas to Extend
- Add extractive mode (TextRank) for comparison
- Summarize YouTube transcripts or web URLs
- Bullet-point summaries using an LLM API
