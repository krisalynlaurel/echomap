# EchoMap – Room Acoustic Studio

EchoMap is a **browser-based acoustic-position testing prototype**. Create a room, mark positions, record a noise baseline and reference test signal, compare relative measurements, and visualise a room heatmap.

## Live application

GitHub Pages project URL: https://krisalynlaurel.github.io/echomap/

**Note:** This URL works only after GitHub Pages is enabled and deployment completes successfully.

## What works

- Interactive room dimensions and position markers
- Microphone selection and guided noise/test-signal capture
- Generated tone or sine sweep, WAV export
- Relative digital noise level (dBFS), SNR estimate, FFT spectral centroid
- Heuristic ranking, position heatmap, sample-results mode
- Browser localStorage for settings/results, JSON export, print-to-PDF
- Web manifest and service worker for basic installable/offline shell

## Start locally

From the project directory, run `python -m http.server 8000`, then open http://localhost:8000 in Chrome or Edge.

The deployed HTTPS site is needed for reliable browser microphone permissions; allow access when prompted.

## Acoustic measurement limitations

This is a **prototype, not a calibrated acoustic meter**. Validated RT60/reverberation estimation is not implemented. Keep microphone position/orientation, speaker location, volume and recording settings consistent for comparisons. Browser or device audio processing can bias metrics. Score weights are experimental and should not be interpreted as validated speech-quality scores. The heatmap is a representation of sampled positions, not comprehensive measurements across the whole room.

Metadata is stored in the user's browser; WAV files are not synced to a server. Clearing browser storage may remove results. Export important files separately.

## Deployment

`.github/workflows/deploy.yml` publishes the root of `main` to GitHub Pages. In the repository, choose **Settings → Pages → Source: GitHub Actions**. View deployment under the Actions tab.