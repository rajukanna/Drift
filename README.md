# Drift — Offline Wind-down Companion 🌙

A serene bedtime companion that generates calming bedtime stories and procedural ambient soundscapes, running **100% offline** directly inside your browser. No accounts, no cookies, no external audio files, and zero network calls.

---

## Architecture Overview

```text
Drift (offline wind-down companion)
├── UI layer  → index.html (single file, no external dependencies)
│   ├── Story tab      → sanctuary setting, custom name, length, font sizing, "Read aloud"
│   └── Soundscape tab → 6 procedural layers, volume sliders, atmospheric presets, sleep timer & fade
├── Logic layer (in-browser JS)
│   ├── Story engine   → themes + generative grammar templates + breathing cues, progressive slowing toward sleep
│   ├── Audio engine   → procedural noise buffers + biquad filters + LFOs (rain, ocean, wind, fire, crickets, hum)
│   └── Read aloud     → device speechSynthesis with soothing cadence & sentence pacing
├── Offline layer
│   ├── sw.js          → pre-caches index.html and assets on first visit with stale-while-revalidate
│   └── manifest.json  → installable PWA for home screen & desktop
└── Hosting → Render Static Site (free, zero server code required)
```

---

## Key Features

### 1. 📖 Bedtime Story Engine
- **6 Sanctuary Settings**: Whispering Pine Forest, Moonlit Ocean Shore, Starlit Alpine Meadow, Cozy Hearth & Cabin, Hilltop Stargazer, and Rainy Bamboo Garden.
- **Sleep-Inducing Pacing**: Sentences and structure progressively slow down as the story nears its end, easing the mind from wakefulness into rest.
- **Integrated Breathing Cues & 4-7-8 Orb**: Gentle breathing cues woven seamlessly between paragraphs and an interactive visual breathing orb.
- **Natural Device Read-Aloud**: Uses `window.speechSynthesis` with intelligent detection of natural, soothing voices, gentle pacing (0.85x), and tranquil pauses between sentences.

### 2. 🎧 6-Layer Procedural Audio Engine
Generates soothing, infinite ambient noise mathematically via the **Web Audio API** without downloading or streaming MP3s:
1. **🌧️ Gentle Rain**: White noise through highpass (850Hz) and lowpass (6000Hz) dual-filter cascade.
2. **🌊 Moonlit Ocean**: Brown noise modulated by an ultra-slow 0.07Hz LFO simulating a 14-second rhythmic wave swell.
3. **🍃 Night Wind**: Bandpass-filtered pink noise swept with gentle organic frequency variation.
4. **🔥 Cozy Campfire**: Sub-frequency brown noise rumble coupled with procedural transient burst micro-crackles.
5. **🦗 Summer Crickets**: Dual tuned sine oscillators (4250Hz - 4400Hz) pulsed in natural clusters.
6. **〰️ Celestial Drone**: 108Hz + 114Hz tuned sine drone creating a therapeutic 6Hz theta relaxation beat combined with sub-bass warmth.
- **Atmospheric Presets**: Quick 1-click presets (*Midnight Rain*, *Cozy Hearth*, *Moonlit Shore*, *Celestial Drone*, *Forest Evening*).
- **Sleep Timer with Gentle Fade**: Configurable timer (15, 30, 45, 60, 90 min) with exponential/linear fadeout over the final minutes to avoid abrupt silence.

### 3. 📱 100% Offline PWA (Progressive Web App)
- Works completely offline (in airplane mode, remote cabins, or nightstand tablets).
- `sw.js` pre-caches all assets.
- Installable directly to home screens on iOS Safari and Android Chrome with custom app icons and standalone display mode.

---

## Deploying to Render Static Site (Free)

Deploying Drift to Render takes under 2 minutes:

1. Push this repository to GitHub or GitLab.
2. Log in to [Render Dashboard](https://dashboard.render.com/).
3. Click **New +** → **Static Site**.
4. Connect your repository.
5. Configure settings (or let `render.yaml` configure them automatically):
   - **Name**: `drift-companion`
   - **Branch**: `main`
   - **Build Command**: *(leave empty)*
   - **Publish Directory**: `.`
6. Click **Create Static Site**.
7. Render will provide a free `https://drift-companion.onrender.com` URL with free SSL and CDN caching!

---

## Local Development & Testing

You can run Drift locally with any static web server:

```bash
# Using Node (npx)
npx serve .

# Or using Python
python -m http.server 8080
```

Open `http://localhost:8080` in your browser.
