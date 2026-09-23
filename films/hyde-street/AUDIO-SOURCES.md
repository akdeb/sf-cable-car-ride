# Audio sources

Everything in the Hyde Street soundscape is procedural except one recording.

## Western Gull, Golden Gate National Recreation Area

- Source: [Wikimedia Commons, *Western Gull Golden Gate National Recreation Area.ogg*](https://commons.wikimedia.org/wiki/File:Western_Gull_Golden_Gate_National_Recreation_Area.ogg)
- Author: National Park Service
- License: public domain (a work of the U.S. federal government)
- Original: 4.65 s, Ogg Vorbis, 44.1 kHz mono
- Changes: high-passed twice at 380 Hz (removes wind rumble), low-passed at 9 kHz, 20 ms fade in
  and 120 ms fade out, peak-normalised to −0.4 dBFS, resampled to 22.05 kHz, stored as base64
  16-bit little-endian PCM in `index.html` (`<script id="gull-rec">`).
- Use: short runs of the laughing call (0.66–1.1 s) placed from 77 s to the end, at playback
  rates 0.94–1.06, panned, filtered and reverberated by distance (`scoreWorld`).

## Reference only (not embedded)

- *Cable Car Big 19 making those cable car sounds.mp3*, supplied by the director. It was analysed
  for spectrum, level swell, clank rate and bell partials; the ride sound is synthesised to match.
