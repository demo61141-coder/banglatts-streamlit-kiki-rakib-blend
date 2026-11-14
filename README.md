# Kiki-Rakib Blend — Streamlit demo

Bengali text-to-speech demo for the **Kiki-Rakib Blend** voice
(a 50/50 weight blend of two single-speaker VITS models, both fresh from
the EMTIAZZ base: Kiki v2 — 2,528 clips, 70 epochs, best step 18307 —
and Rakib v2 — 2,362 clips, 65 epochs, best step 17141).

Open the app, type or paste Bengali text, press **অডিও বানাও**, listen,
download the WAV.

## How the model loads

The 114 MB ONNX model is NOT in this repo (GitHub's 100 MB per-file
limit). On first run the app downloads it from Hugging Face and verifies
exact byte size AND MD5 before use, then caches it:

- Model: https://huggingface.co/demoqqq/banglatts-kiki-rakib-blend/resolve/main/model.onnx
- Tokens: https://huggingface.co/demoqqq/banglatts-kiki-rakib-blend/resolve/main/tokens_sherpa.txt

## Files

- `app.py` — Streamlit UI (Bengali): text input, sample texts, speed
  selector, Generate, audio player, WAV download.
- `tts_engine.py` — synthesis engine (sherpa-onnx): danda-based chunking
  (≤700 chars/part), 0.5 s joins, 22050 Hz mono output, Kiki orthography
  normalization (য়→য+়, ড়→ড+়, ঢ়→ঢ+়) before generation.
- `requirements.txt` — sherpa-onnx 2.0.1, streamlit, numpy.

## Notes

- The blend vocab (92 tokens, identical in both parents) uses ONLY decomposed forms (য+়/ড+়/ঢ+়),
  so typed Bengali is normalized before generation (see normalize_text()
  in tts_engine.py). This is the documented Kiki orthography rule.
- Model constants verified at finish: model.onnx 114,192,755 bytes
  (MD5 26d60c69dc681909ed39b066da681ff6); tokens_sherpa.txt 605 bytes
  (MD5 366751e11c26877a07828e4cbd3e7d7d).
