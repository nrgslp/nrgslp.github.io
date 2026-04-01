---
layout: single
title: "Speech Inversion Service — User Guide"
permalink: /si-service-guide26/
author_profile: true
toc: true
toc_label: "On this page"
toc_icon: "file-alt"
noindex: true
---

**Interpretable and Available Acoustic-to-Articulatory Speech Inversion**
*Funded by the ASHFoundation New Investigators Research Grant*
*PI: Nina R. Benway, PhD CCC-SLP · University of Maryland, College Park*

---

## What Is This Service?

The Speech Inversion Service estimates how the vocal tract is moving during speech. 

These estimates are called **tract variables**, a framework from Articulatory Phonology (Browman & Goldstein, 1992). Tract variables describe articulator movements at 100 frames per second (every 10 milliseconds).

The models currently available are based on the Siriwardena speech inversion system (Siriwardena & Espy-Wilson, ICASSP 2023; Siriwardena, Sivaraman, & Espy-Wilson, 2022), trained on adult speaker articulography data from the Wisconsin Xray Microbeam Dataset. **Additional models are in development** and will be added to the service over time, including models trained on child speech and models with phonetically normalized tract variables.

---

## Who Is This For?

This service is designed for speech researchers who want acoustic-to-articulatory speech inversion estimates for research purposes. 

If you use data from clinical populations (e.g., children with speech sound disorders), please ensure your IRB protocol covers secondary data use. 

---

## What You Will Receive

For each `.wav` file you submit, you will receive one **CSV file** (openable in Excel, MATLAB, R, SPSS, or Python) containing tract variable estimates over time.

**Example output** (XRMB model, first 3 rows):

| frame | time_s | LA | LP | TTCL | TTCD | TBCL | TBCD |
|---|---|---|---|---|---|---|---|
| 0 | 0.000 | 0.2342 | −0.1180 | 0.4453 | −0.3321 | 0.1121 | −0.5679 |
| 1 | 0.010 | 0.2410 | −0.1124 | 0.4390 | −0.3279 | 0.1183 | −0.5609 |
| 2 | 0.020 | 0.2489 | −0.1063 | 0.4321 | −0.3231 | 0.1248 | −0.5534 |

**Column definitions:**

| Column | Full Name | Description |
|---|---|---|
| `frame` | Frame index | Time step (0-indexed, 100 Hz) |
| `time_s` | Time in seconds | Frame 0 = 0.000 s, Frame 1 = 0.010 s, etc. |
| `LA` | Lip Aperture | Vertical distance between upper and lower lip |
| `LP` | Lip Protrusion | Forward extension of the lips |
| `TTCL` | Tongue Tip Constriction Location | How far forward/back the tongue tip constriction is |
| `TTCD` | Tongue Tip Constriction Degree | How close the tongue tip is to the palate |
| `TBCL` | Tongue Body Constriction Location | How far forward/back the tongue body constriction is |
| `TBCD` | Tongue Body Constriction Degree | How close the tongue body is to the palate |

The **HPRC model** additionally estimates:

| Column | Full Name | Description |
|---|---|---|
| `PER` | Periodicity | Degree of periodic (voiced) voicing |
| `APER` | Aperiodicity | Degree of aperiodic (noisy) voicing |
| `F0` | Fundamental Frequency | Estimated pitch in Hz |
| `phone_label` | Phoneme label | Predicted phoneme symbol for each frame |

You will also receive a `run_metadata.json` file documenting the model used, processing results, and full citation information for your records.

---

## Before You Begin

### Audio file requirements

- **Format:** WAV files only (`.wav`)
- **Sample rate:** Any — files are automatically converted to 16 kHz
- **Duration:** At least 100 milliseconds per file; no maximum
- **Content:** Any speech is acceptable. The service does not reject recordings based on speaker characteristics, dialect, disorder type, or recording quality.
- **Channels:** Mono preferred; stereo files are automatically converted to mono

### What to avoid

- Non-speech audio (music, noise-only recordings) will produce output but the estimates will not be meaningful
- Files shorter than 100 ms will be rejected with an error message
- Files in formats other than `.wav` (e.g., `.mp3`, `.m4a`) will be rejected — please convert them first

---

## How to Submit

### Step 1 — Prepare your audio files

Collect all `.wav` files for a single batch into one folder, then compress it into a ZIP file.

**On Windows:** Right-click the folder → *Send to* → *Compressed (zipped) folder*
**On Mac:** Right-click the folder → *Compress*

The ZIP file can contain up to several hundred files. Each is processed separately.

### Step 2 — Open the submission form

Go to: https://redcap.link/si-service

### Step 3 — Complete the form

The form will ask for:

1. **Your email address** — results will be sent here
2. **Your ZIP file** — the compressed folder of `.wav` files
3. **Model selection** — which speech inversion model to use (see below)
4. **Password** - a password generated for you by Nina R Benway. 

Once submitted, you will receive a confirmation with your **Job ID**. Keep this for your records.

### Step 4 — Wait for your results

You will receive an **email** when results are ready. The email contains a **download link** valid for **7 days**, after which files are automatically deleted per our data retention policy.

---

## Choosing a Model

| Model | Best for | Output columns |
|---|---|---|
| **XRMB** *(recommended for most users)* | Adult speech; general articulation research | frame, time_s, LA, LP, TTCL, TTCD, TBCL, TBCD |
| **HPRC** | Research requiring voicing/pitch estimates or phoneme labels | All XRMB columns + PER, APER, F0, phone_label |

**Not sure which to choose?** Select XRMB. It was trained on a larger dataset (46 adult speakers from the Wisconsin X-Ray Microbeam Database) and provides the six core Articulatory Phonology tract variables.

New models are coming soon.

---

## Data Privacy and HIPAA

- Audio files are **encrypted in transit** (HTTPS) and **at rest** (AES-256)
- Audio files are **automatically deleted after 7 days**. CSV output files (numbers only, no audio) may be retained longer
- Only the submitting researcher receives the download link
- Server logs do **not** record filenames or email addresses — only an anonymous Job ID
- This service is hosted on University of Maryland infrastructure

**If your audio contains recordings from human participants:**
Please ensure your IRB protocol covers submission of de-identified audio to a third-party analysis service.

---

## Troubleshooting

**I received an error for one of my files.**
The results email will specify which file(s) failed and what to fix. Other files in your batch are still processed. Common causes:
- The file is not a valid WAV — try re-exporting from your recording software
- The file is shorter than 100 ms
- The file contains no audio signal (silence only)

**My download link has expired.**
Links are valid for 7 days. Please resubmit your files.

**The results don't look right.**
Tract variable estimates are most reliable for clearly recorded speech at a comfortable speaking rate. Very fast speech, overlapping speakers, or noisy recordings may produce less reliable estimates. This is a model limitation, not an error.

**I need help interpreting the output.**
See the references below.

---

## Citation

If you use this service in published research, please cite:

> Benway, N. R. (in preparation). Speech Inversion Service [Software]. University of Maryland.

And the underlying model:

> Siriwardena, L., Sivaraman, G., & Espy-Wilson, C. (2022). Multitask learning for acoustic-to-articulatory speech inversion. *arXiv:2205.13755*.
> Siriwardena, L., & Espy-Wilson, C. (2023). Acoustic-to-articulatory speech inversion using self-supervised speech representations. *ICASSP 2023*.

---

## References

- Browman, C. P., & Goldstein, L. (1992). Articulatory Phonology: An overview. *Phonetica, 49*(3–4), 155–180.
- Chen, S., Wang, C., Chen, Z., et al. (2022). WavLM: Large-scale self-supervised pre-training for full stack speech processing. *IEEE Journal of Selected Topics in Signal Processing, 16*(6), 1505–1518.

---

## Contact

Nina R. Benway, PhD CCC-SLP
Postdoctoral Fellow, Electrical and Computer Engineering
University of Maryland, College Park

*This service is available for research use, with funding for ~ 4 years following initial deployment.*
