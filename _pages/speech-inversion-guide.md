---
layout: single
title: "Speech Inversion Service User Guide"
permalink: /si-service-guide26/
author_profile: true
noindex: true
hidden: true
---

<style>
details {
  border: 1px solid #dcdcdc;
  border-radius: 8px;
  padding: 0.6em 1em;
  margin: 1em 0;
  background: #fafafa;
}
details > summary {
  cursor: pointer;
  font-weight: 600;
  list-style: none;
  position: relative;
  padding-left: 1.3em;
}
details > summary::-webkit-details-marker { display: none; }
details > summary::before {
  content: "\25B8";
  position: absolute;
  left: 0;
  transition: transform 0.15s ease-in-out;
  display: inline-block;
}
details[open] > summary::before {
  transform: rotate(90deg);
}
details > summary + * {
  margin-top: 0.8em;
}
</style>

**Interpretable and Available Acoustic-to-Articulatory Speech Inversion**
*Funded by the ASHFoundation New Investigators Research Grant*
*PI: Nina R. Benway, PhD CCC-SLP · University of Maryland, College Park*

---

## What Is The Speech Inversion Service?

The Speech Inversion Service is a web interface for acoustic-to-articulatory speech inversion neural network models. Acoustic-to-articulatory speech inversion infers how the vocal tract is moving during speech, using the audio alone (more on this below). These inferences are built upon vocal tract variables, a standard framework from Articulatory Phonology (Browman & Goldstein, 1992). The values of vocal tract variables describe the state of the vocal tract through articulator constriction location and degree at 100 frames per second (every 10 milliseconds).

The Speech Inversion Service uses the WavLM-Nasality model (Tabatabaee et al., 2025), which estimates 10 acoustic-to-articulatory channels simultaneously, including `nasalance`.

To use the service, submit audio recordings, and within one hour you receive a data file describing the movements of articulators (lips, tongue tip, tongue body) over time, along with estimates of nasality and voicing characteristics.

Before using the service, please ensure your IRB protocol covers your intended use/secondary use of your data, including upload of speech to a third-party analysis service. More details can be found in the Data Privacy section below.

---

<details markdown="1">
<summary>What Is Speech Inversion and What Are Tract Variables?</summary>

Speech inversion estimates articulatory movement directly from the acoustic signal (e.g., Papcun et al., 1992), without any imaging or sensors on the speaker. This makes it possible to approximate kinematic analysis in datasets that were never collected with kinematic instrumentation.

Our Speech Inversion Systems are neural networks trained to map speech audio onto kinematic ground truth. That ground truth typically comes from articulography: X-ray microbeam or electromagnetic systems that track pellets or sensors glued to the lips and tongue (Westbury et al., 1994; Rebernik et al., 2021). Our team's systems were trained on the Wisconsin X-ray Microbeam (XRMB) dataset, which contains American English.

This service has not been validated on languages other than English. We expect it to generalize reasonably well to languages with a phonological feature distribution similar to English's, and there is early evidence supporting that: an adult speech inversion system trained only on English data recovered tract variables in French and Russian with average correlations of .83 and .74 against articulatory ground truth, respectively. One caveat: the XRMB training data has limited coverage of back-of-tongue (dorsal) articulation, so model performance might generalize least to languages with a different distribution of dorsal productions than English.

Rather than predicting a sensor's raw (X, Y) position in millimeters, the model predicts normalized tract variables, constriction location and constriction degree, following the Articulatory Phonology framework (Browman & Goldstein, 1992). This normalization helps tract variables generalize across speakers better than raw sensor coordinates, which shift with anatomical differences in vocal tract size (Mitra et al., 2010).

Six tract variables describe the vocal tract: lip aperture, lip protrusion, tongue tip constriction location, tongue tip constriction degree, tongue body constriction location, and tongue body constriction degree. This service also predicts three source variables describing the glottal source: fundamental frequency, periodic energy, and aperiodic energy. Adding source variables improves the accuracy of the vocal tract gesture estimates themselves (Deshmukh et al., 2005; Siriwardena & Espy-Wilson, 2023), likely because they provide timing information that constrains gesture estimation and capture nonlinear interactions between the glottal source and the vocal tract filter.

<details markdown="1">
<summary>Model accuracy on the XRMB test set (Pearson's <em>r</em>)</summary>

Reported by Tabatabaee et al. (2025), Table 3, MTL-SI/WavLM-Large row, against articulography ground truth for adult speakers:

| `nasalance` | `PER` | `APER` | `F0` | `LA` | `LP` | `TBCL` | `TBCD` | `TTCL` | `TTCD` |
|---|---|---|---|---|---|---|---|---|---|
| .946 | .940 | .882 | .747 | .910 | .759 | .798 | .863 | .836 | .948 |

</details>

<details markdown="1">
<summary>How constriction location and degree are computed (technical detail)</summary>

Attia et al. (2024) describe how constriction location and degree are computed from the XRMB pellets used as ground truth. XRMB tracks four tongue pellets (T1, nearest the tip, through T4, nearest the tongue dorsum), an upper lip pellet (UL), a lower lip pellet (LL), and an incisor reference point.

- Lips: lip aperture is the distance between the UL and LL pellets. Lip protrusion is the horizontal offset of the LL pellet from the incisor.
- Tongue tip: constriction degree is the minimum distance between pellet T1 and the palate trace. Constriction location is the horizontal offset of T1 from the incisor at the point of narrowest constriction.
- Tongue body: constriction degree is the minimum distance between an arc through pellets T2–T4 and the trace of the palate/velum/pharyngeal wall. Constriction location is the horizontal offset of that arc from the incisor at the point of narrowest constriction.

</details>

</details>

---

## Who Is The Speech Inversion Service For?

This service is designed for speech researchers who want acoustic-to-articulatory speech inversion estimates for research purposes (i.e., not commercial purposes).

---

## Speech Inversion Service Output

For each `.wav` file you submit, you will receive one output file containing tract variable estimates over time. The default format is CSV (spreadsheet), which can be opened in Excel, MATLAB, R, SPSS, or Python.

*Example output* (WavLM-Nasality model, first 3 rows):

| frame | time_s | nasalance | PER | APER | F0 | LA | LP | TBCL | TBCD | TTCL | TTCD |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0.000 | 0.123 | 0.456 | 0.012 | −0.234 | 0.344 | −0.118 | 0.133 | −0.332 | 0.445 | −0.568 |
| 1 | 0.010 | 0.131 | 0.461 | 0.011 | −0.228 | 0.351 | −0.112 | 0.139 | −0.328 | 0.439 | −0.561 |
| 2 | 0.020 | 0.140 | 0.470 | 0.009 | −0.219 | 0.359 | −0.106 | 0.146 | −0.323 | 0.432 | −0.553 |

<details markdown="1">
<summary>Column definitions</summary>

| Column | Full Name | Description |
|---|---|---|
| `frame` | Frame index | Time step (0-indexed). Frame 0 = 0 ms, Frame 1 = 10 ms, etc. |
| `time_s` | Time (seconds) | Time in seconds corresponding to each frame |
| `nasalance` | Nasalance | Estimated degree of nasal resonance (raw model output, not a probability) |
| `PER` | Periodicity | Degree of periodic (voiced) voicing |
| `APER` | Aperiodicity | Degree of aperiodic (noisy) voicing |
| `F0` | Fundamental Frequency | Estimated pitch |
| `LA` | Lip Aperture | Vertical distance between upper and lower lip |
| `LP` | Lip Protrusion | Forward extension of the lips |
| `TTCL` | Tongue Tip Constriction Location | How far forward/back the tongue tip constriction is |
| `TTCD` | Tongue Tip Constriction Degree | How close the tongue tip is to the palate |
| `TBCL` | Tongue Body Constriction Location | How far forward/back the tongue body constriction is |
| `TBCD` | Tongue Body Constriction Degree | How close the tongue body is to the palate |

</details>

*Note on scale:* Tract variable values are normalized, unitless model outputs. They are not in centimeters or millimeters. They represent relative articulatory positions that can be compared within and across speakers.

---

## Using the Speech Inversion Service

<details markdown="1">
<summary>Before You Begin</summary>

Audio file requirements

- Format: WAV files only (`.wav`)
- Sample rate: any sample rate is accepted; files are automatically converted to 16 kHz. Uploading your audio at 16 kHz, though not required, will allow you to upload more audio per batch.
- Duration: at least 100 milliseconds per file, no maximum
- Content: any speech is acceptable. The service does not reject recordings based on speaker characteristics, dialect, disorder type, or recording quality.
- Channels: mono preferred; stereo files are automatically converted to mono

What to avoid

- Non-speech or low-quality audio files (music, noise-only recordings) will produce output, but the estimates will not be meaningful (e.g., "garbage in, garbage out")
- Files shorter than 100 ms will be rejected with an error message
- Files in formats other than `.wav` (e.g., `.mp3`, `.m4a`) will be rejected; please convert them first

</details>

<details markdown="1">
<summary>How to Submit</summary>

Step 1 — Prepare your audio files

- If you have just one recording, you can upload the single `.wav` file directly; no zipping needed.
- For multiple files, collect all `.wav` files for a batch into one folder on your computer, then compress that folder into a single ZIP file:
- On Windows: Right-click the folder → *Send to* → *Compressed (zipped) folder*. On Mac: Right-click the folder → *Compress*
- The ZIP file can contain up to several hundred files. Each file will be processed separately.

Step 2 — Complete the REDCap submission form

The form will ask for:

- Your email address: results will be sent here when processing is complete
- Your audio: upload a single `.wav` file, or a ZIP of `.wav` files
- Output format: choose CSV (default), TXT, or NPY (NumPy binary)
- Once you submit, you will see a confirmation message with your Job ID. Keep this for your records.

Step 3 — Wait for your results

- Processing time depends on the number and length of files in your batch, as well as the length of the job queue. You will receive an email when your results are ready, typically within one hour. Note that the first job of the day takes a little longer as the system wakes up.
- The email will contain a download link for a ZIP of your result files. This link is valid for 7 days. After 7 days, the results are automatically deleted from our servers in accordance with our data retention policy.

</details>

---

<details markdown="1">
<summary>Output Format Options</summary>

| Format | Description | Best for |
|--------|-------------|----------|
| CSV (default) | Comma-separated with header row | Excel, MATLAB, R, SPSS |
| TXT | Tab-separated with header row; same content as CSV | Viewing output alongside its input waveform in Wavesurfer |
| NPY | NumPy binary array, shape `[n_frames, 10]`, no header | Python users; load with `numpy.load()` |

For NPY files, the channel order is `nasalance`, `PER`, `APER`, `F0`, `LA`, `LP`, `TBCL`, `TBCD`, `TTCL`, `TTCD`. This order is also documented in `run_metadata.json`, included in the results ZIP.

</details>

---

<details markdown="1">
<summary>Data Privacy</summary>

- Audio files are encrypted in transit (HTTPS) and encrypted at rest on our servers (AES-256 encryption)
- Audio files are automatically deleted after 7 days. The output files (which contain only numbers, not audio) may be retained longer
- Only you (the submitting researcher) receive the download link; results are not shared with other users
- Our server logs record only a job ID, not your audio filenames or researcher email address
- This service is hosted on authorization-based infrastructure at the University of Maryland
- *Please ensure your IRB protocol covers upload of speech to a third-party analysis service.*

</details>

---

<details markdown="1">
<summary>Troubleshooting</summary>

*My email is not on the Speech Inversion Service allowlist.*
Email Nina Benway to request access. Please note that should demand outpace the available funding to run the website, priority access may be given to clinical researchers studying communication disorders.

*I received an error for one of my files.*
The email summary will tell you which file(s) failed and why. Common reasons:
- The file is not a valid WAV (try re-exporting from your audio software)
- The file is shorter than 100 ms
- The file contains no audio signal (silence only)

Other files in your batch are still processed even if one file fails.

*My download link has expired.*
Download links are valid for 7 days. If your link has expired, please resubmit your files.

*The results don't look right.*
Tract variable estimates are most reliable for clearly recorded speech at a comfortable speaking rate. Very fast speech, overlapping speakers, or very noisy recordings may produce less reliable estimates. This is a limitation of the underlying model, not an error.

One way to sanity-check output on a few files: load the trajectories in a tool like WaveSurfer alongside the audio, and screen for basic phonological plausibility. Constrictions should be timed with the audio (e.g., a stop consonant should show closure and burst where you can see and hear one), and the articulator involved should match place of articulation (e.g., bilabials should show a lip constriction, alveolars a tongue tip constriction). This works best on a handful of perceptually clear target files, and is more informative than trying to judge a whole batch at once.

</details>

---

<details markdown="1">
<summary>Citing the Speech Inversion Service</summary>

If you use this service in published research, please cite at least the following papers:

> Benway, N. R., Tabatabaee, S., Wang, D., Munson, B., Preston, J. L., & Espy-Wilson, C. (2026). Perceptual ratings predict speech inversion articulatory kinematics in childhood speech sound disorders. *Journal of Speech, Language, and Hearing Research*, 69(2), 541–561. https://doi.org/10.1044/2025_JSLHR-25-00515

> Tabatabaee, S., Boyce, S., Oren, L., Tiede, M., & Espy-Wilson, C. (2025). Enhancing Acoustic-to-Articulatory Speech Inversion by Incorporating Nasality. *Proc. Interspeech 2025*, 325–329. https://doi.org/10.21437/Interspeech.2025-2387

**References**

- Attia, A. A., Siriwardena, Y. M., & Espy-Wilson, C. (2024). Improving speech inversion through self-supervised embeddings and enhanced tract variables. *2024 32nd European Signal Processing Conference (EUSIPCO)*, 306–310.
- Browman, C. P., & Goldstein, L. (1992). Articulatory Phonology: An overview. *Phonetica, 49*(3–4), 155–180.
- Chen, S., Wang, C., Chen, Z., et al. (2022). WavLM: Large-scale self-supervised pre-training for full stack speech processing. *IEEE Journal of Selected Topics in Signal Processing, 16*(6), 1505–1518.
- Deshmukh, O., Espy-Wilson, C. Y., Salomon, A., & Singh, J. (2005). Use of temporal information: Detection of periodicity, aperiodicity, and pitch in speech. *IEEE Transactions on Speech and Audio Processing, 13*(5), 776–786.
- Mitra, V., Nam, H., Espy-Wilson, C. Y., Saltzman, E., & Goldstein, L. (2010). Retrieving tract variables from acoustics: A comparison of different machine learning strategies. *IEEE Journal of Selected Topics in Signal Processing, 4*(6), 1027–1045.
- Oohashi, H., Watanabe, H., & Taga, G. (2017). Acquisition of vowel articulation in childhood investigated by acoustic-to-articulatory inversion. *Infant Behavior and Development, 46*, 178–193.
- Papcun, G., Hochberg, J., Thomas, T. R., Laroche, F., Zacks, J., & Levy, S. (1992). Inferring articulation and recognizing gestures from acoustics with a neural network trained on X-ray microbeam data. *The Journal of the Acoustical Society of America, 92*(2), 688–700.
- Rebernik, T., Jacobi, J., Jonkers, R., Noiray, A., & Wieling, M. (2021). A review of data collection practices using electromagnetic articulography. *Laboratory Phonology, 12*(1), Article 6.
- Serkhane, J., Schwartz, J.-L., Boë, L.-J., Davis, B. L., & Matyear, C. L. (2007). Infants' vocalizations analyzed with an articulatory model: A preliminary report. *Journal of Phonetics, 35*(3), 321–340.
- Siriwardena, Y. M., Boyce, S. E., Tiede, M. K., Oren, L., Fletcher, B., Stern, M., & Espy-Wilson, C. Y. (2024). Speaker-independent speech inversion for recovery of velopharyngeal port constriction degree. *The Journal of the Acoustical Society of America, 156*(2), 1380–1390.
- Siriwardena, Y. M., & Espy-Wilson, C. (2023). The secret source: Incorporating source features to improve acoustic-to-articulatory speech inversion. *ICASSP 2023 – 2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)*, 1–5.
- Tabatabaee, S., Boyce, S., Oren, L., Tiede, M., & Espy-Wilson, C. (2025). Enhancing Acoustic-to-Articulatory Speech Inversion by Incorporating Nasality. *arXiv:2506.09231*.
- Westbury, J. R., Turner, G., & Dembowski, J. (1994). *X-ray microbeam speech production database user's handbook*. University of Wisconsin.

</details>

---

*This service is available for research use until funding is exhausted.*
