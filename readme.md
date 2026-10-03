# Reel to Shop

Turning video reel frames into **search-ready product catalogue entries** using Gemini's multimodal vision.

The idea: someone watches a fashion reel, likes the jacket, and has no way to find it. This pipeline looks at the frame, identifies each product in it, and emits structured JSON good enough to feed straight into a product search.

---

## Pipeline

```
Reel frames / images
    │
    ▼
Gemini 2.5 Flash  ──► visual analysis prompt
    │                  identify every distinct product in frame
    ▼
image_analysis_results.json      ← raw model output per image
    │
    ▼
Refinement pass   ──► normalise into consistent, queryable fields
    │
    ▼
search_ready_products.json       ← catalogue-ready records
```

Two stages on purpose. The first pass is deliberately open-ended so the model describes everything it sees without being squeezed into a schema too early. The second pass cleans that into consistent fields so the output is actually queryable.

---

## Stack

Google Gemini 2.5 Flash (multimodal) · Python · Jupyter / Google Colab

---

## Running it

```bash
pip install google-generativeai
```

Open `eena.ipynb` in Colab or Jupyter, set your `GOOGLE_API_KEY`, then upload images when the cell prompts you.

Outputs land as:
- `image_analysis_results.json` — raw per-image analysis
- `search_ready_products.json` — normalised product records

---

## Status

Research notebook — the extraction half of a shoppable-video concept. The consumer-facing app built on this idea is [reelstyle-shopper](https://github.com/Mp17082005/reelstyle-shopper).
