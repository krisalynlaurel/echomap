# EchoMap v0.3 – Acoustic Room Studio

**Live web app:** https://krisalynlaurel.github.io/echomap/

EchoMap is a browser-based academic acoustic testing tool that compares **relative** audio quality at different microphone positions in a room. It is not a certified acoustic meter.

## Features
- Responsive dashboard and interactive 2D room map with up to 26 position markers
- Multiple rooms and dated testing sessions, saved locally
- Guided microphone measurement with 2/3/5 second ambient-noise baseline and a 3-second 400–3500 Hz logarithmic sweep or 440 Hz tone
- Playback signal and 1.5-second decay tail capture; downloadable 16-bit mono WAV
- Digital RMS/noise dBFS, estimated SNR, clipping/quality checks, FFT-based spectral centroid and five sweep-reference-adjusted frequency bands
- Experimental decay-tail proxy when quality is adequate — **not validated RT60**, not used for scoring
- Repeat trials with mean and sample variation; invalid trials are excluded from ranking
- Heuristic weighted position ranking and sample-only marker heatmap
- A/B playback from locally saved WAVs, plus JSON/CSV export and printable PDF report
- Browser localStorage and IndexedDB for persistence, installable PWA shell and limited offline support
- Node unit tests in `tests/dsp.test.mjs` and GitHub Actions validation before deployment

## How to test

1. Open the hosted HTTPS page or run `python -m http.server 8000` then visit `http://localhost:8000`.
2. Create or select a room, set dimensions, add positions.
3. Keep speaker location/volume fixed; move microphone between positions. Use Chrome or Edge and approve microphone permission.
4. At each position, capture **three or more** trials using the same test signal and input settings.
5. Review trial quality, frequency bands and ranking; listen back to recorded WAV files using A/B playback.
6. Export the JSON or CSV and print a PDF under Reports.

Sample data can be loaded for a no-microphone demonstration. It is saved into a separate clearly labelled session and has no WAV clips.

## Limitations and science notes

- Browser dBFS is a digital relative amplitude, **not calibrated dB SPL**.
- Microphone, loudspeaker, gain control, acoustic noise, playback latency and device characteristics change results. The app requests echo cancellation, noise suppression and automatic gain control be disabled but cannot guarantee the device honours these settings.
- Frequency bands are derived from a reference sweep and are rough comparative features, not flat calibrated frequency responses.
- Decay-tail time is an experimental fit to post-sweep amplitude. **It is not a standard T20/T30/RT60 room reverberation measurement and is intentionally excluded from score.** Unreliable decays are reported as unavailable.
- Scores are experimental, relative to tested positions and their measured signal/noise, rather than validated speech quality. Coloured marker halos do not interpolate sound quality over unmeasured floor locations.
- The room floor and dimensions are metadata and map context, not acoustic prediction inputs.
- Audio is recorded/stored only in browser IndexedDB, not on GitHub or a server. The user can download WAVs, and clearing browser data removes stored files. Safari / private browsing may restrict storage. Legacy v0.1 measurements can be imported where their metadata is present, but their audio cannot be recovered.
- No user accounts, backend database, calibrated equipment support or validated speech intelligibility index is included.

## Development

Requires Node 22+ only for testing; no bundler or dependency installation is needed.

```sh
npm test
node --check app.js
python -m http.server 8000
```

The web app itself is plain HTML, CSS, and JavaScript modules. GitHub Pages automatically publishes `main` via `.github/workflows/deploy.yml` after testing. Under **Settings → Pages** select **GitHub Actions**.