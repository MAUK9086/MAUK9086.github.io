---
title: "Contactless Vital-Sign Estimation from Video (rPPG)"
excerpt: "Estimating heart rate, heart-rate variability and SpO2 from an ordinary webcam using remote photoplethysmography, as part of the &ldquo;Walk for Life&rdquo; project at the Institute of Liver and Biliary Sciences, New Delhi (2026–present). Public prototypes: SerenePulse and an in-browser HRV dashboard."
collection: portfolio
order: 2
permalink: /portfolio/contactless-vital-signs
---

**Context:** Machine Learning Intern, "Walk for Life" project, Institute of Liver and Biliary Sciences (ILBS), New Delhi, January 2026 – present.
**Project leads:** Prof. (Dr.) Shiv Kumar Sarin, Director, ILBS, and Senior Professor & Head, Department of Hepatology (Principal Investigator); Dr. Harsh Vardhan T., Associate Professor, Department of Hepatology (Co-Principal Investigator).
**Public prototypes:** [SerenePulse](https://github.com/MAUK9086/serenepulse) (Python / FastAPI) · [HRV_app](https://github.com/MAUK9086/HRV_app) (TypeScript, runs in the browser)

Background
------
Remote photoplethysmography (rPPG) recovers the blood-volume pulse from subtle colour changes in facial skin recorded by a standard camera. Turning that signal into reliable heart rate (HR), heart-rate variability (HRV) and oxygen saturation (SpO2) estimates requires robust skin-region tracking, handling of motion and illumination, and careful signal processing.

My work at ILBS
------
- **Clinical data engineering:** a pipeline that merges and normalises longitudinal patient records from more than 10 heterogeneous clinical sources.
- **Vital-sign estimation:** real-time HR, HRV and SpO2 estimation from webcam video using rPPG signal processing and computer vision.
- **Systems:** low-latency inter-process communication and data-validation constraints, so concurrent telemetry streams are processed with transactional integrity.

<img src="/images/placeholder-figure.png" alt="Figure forthcoming" width="70%">

Signal-processing pipeline (public prototypes)
------
1. **Region selection:** MediaPipe FaceMesh landmarks define three skin regions of interest (forehead, left cheek, right cheek).
2. **Colour signal:** the mean RGB of each region is combined into a GRGB signal (G/R + G/B), which cancels illumination changes common to all channels. The in-browser version uses the POS (plane-orthogonal-to-skin) projection.
3. **Source separation and filtering:** winsorisation and z-scoring, FastICA, then a 6th-order Butterworth band-pass filter at 0.65–4.0 Hz (39–240 bpm).
4. **Metrics:** BPM from spectral peaks; SDNN, RMSSD and the LF/HF ratio from inter-beat intervals; and a Welch-based signal-to-noise ratio as a quality gate.
5. **Session protocol:** a timed 60-second session (positioning, calibration and live measurement), streamed to the client over WebSockets.

```python
def compute_grgb(roi_rgb_means):
    r, g, b = (np.maximum(roi_rgb_means[:, i], 1e-8) for i in range(3))
    return (g / r) + (g / b)

def rmssd(ibi_sec):
    d = np.diff(ibi_sec); return float(np.sqrt(np.mean(d * d)))
```

The browser version (HRV_app) runs the whole chain on the client: POS extraction in a Web Worker, a hand-written FFT and continuous wavelet transform, and HRV spectral analysis on inter-beat intervals resampled to 4 Hz. No video leaves the device.
