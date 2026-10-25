# Drift — Offline Wind-down Companion 🌙

*This is a submission for the [Hacktoberfest Open-Source AI Challenge Week 3: Slow and Steady](https://dev.to/challenges/hacktoberfest-week3-2026-10-19)*

---

## What I Built

**Drift** is a calming bedtime companion and sleep sanctuary that generates restful bedtime stories and ambient soundscapes, running **100% offline** directly inside your browser.

Modern wind-down apps have become bloated subscription traps requiring logins, credit cards, data tracking, and constant internet access. If you're on a flight, camping off-grid, or simply putting your phone into Airplane Mode to sleep without notifications, closed apps fail.

Drift strips away all the friction:
- **Zero Dependencies, Zero Network Calls**: Everything runs client-side inside a single lightweight web application.
- **Hypnotic Bedtime Story Engine**: Procedurally generates soothing stories across 6 sanctuary settings, dynamically pacing sentences to slow down as you drift toward sleep, interspersed with gentle 4-7-8 breathing cues.
- **Pure Web Audio Ambient Soundscapes**: 6 synthesized sound layers (Rain, Ocean, Night Wind, Campfire, Crickets, and 6Hz Theta Drone) generated mathematically on the fly—no bulky MP3 downloads or audio streaming required.
- **Offline PWA & Sleep Timer**: Installable on iOS/Android home screens with an automatic sleep timer that gently fades audio to complete silence over the final minutes.

**Who gets to be a little lazier because of it?**  
Anyone who wants to fall asleep faster without spending $70/year on subscription apps or fumbling with complex sleep trackers in the dark. You tap one preset, place your phone face down on your nightstand, and let Drift ease you into sleep.

---

## Demo

- **GitHub Repository**: [https://github.com/rajukanna/Drift](https://github.com/rajukanna/Drift)
- **Deployment Live URL**: https://drift-hwi6.onrender.com

### Visual Preview

- **Deep Velvet Twilight UI**: Designed with glassmorphic cards, luminous starlight accents, and a pure Canvas starry backdrop that consumes minimal battery and won't strain tired eyes.
- **Visual Breathing Orb**: A built-in 4-7-8 breath pacer (*Inhale 4s &rarr; Hold 7s &rarr; Exhale 8s*) synchronizes lung capacity with physical relaxation before story reading starts.
- **Bedtime Story Reader**: Clean, book-inspired night typography with `A-` / `A` / `A+` font scaling and synchronized sentence focus highlighting when read aloud.
- **Soundscape Mixer**: 6 distinct procedural layers with dedicated volume sliders, active indicators, instant 1-click presets (*Midnight Rain*, *Cozy Hearth*, *Moonlit Shore*, *Celestial Drone*, *Forest Evening*), and sleep timers.

---

## Code

The entire companion is open-source and structured for absolute simplicity and durability:

```text
Drift (offline wind-down companion)
├── UI layer  → index.html (single file, zero external CDN dependencies)
│   ├── Story tab      → sanctuary setting, custom name, length, font sizing, "Read aloud"
│   └── Soundscape tab → 6 procedural layers, volume sliders, sleep timer & fade
├── Logic layer (in-browser JS)
│   ├── Story engine   → themes + grammar templates + breathing cues, slows toward sleep
│   ├── Audio engine   → noise buffers + biquad filters + LFOs (rain, ocean, wind, fire, crickets, hum)
│   └── Read aloud     → device speechSynthesis (soothing rate & pacing)
├── Offline layer
│   ├── sw.js          → pre-caches index.html and assets on first visit with stale-while-revalidate
│   └── manifest.json  → installable PWA for home screen & desktop
└── Hosting → Render Static Site (render.yaml, free, zero server code)
```

Explore the core source files directly in the repository:
- [`index.html`](index.html) — Single-file UI, generative story grammar, Web Audio synthesizer & speech engine
- [`sw.js`](sw.js) — Service worker providing 100% offline caching and background synchronization
- [`manifest.json`](manifest.json) — Progressive Web App manifest with standalone display configuration
- [`render.yaml`](render.yaml) — Zero-config deployment blueprint for Render Static Sites

---

## How I Built It

Drift was built using open-source web technologies and pair programmed with an agentic AI harness (**Google Antigravity with Gemini 3.8 Flash**).

Instead of relying on remote closed-source APIs that fail offline, Drift was designed from the ground up around **local, device-native browser capabilities**:

1. **Procedural Story Engine (In-Browser Grammar & Pacing)**:
   - Implemented a generative narrative engine structured with customizable sanctuary themes:
     - 🌲 *Whispering Pine Forest* (Pip the fox, ancient pines, mossy brooks)
     - 🌊 *Moonlit Ocean Shore* (Marlow the sea turtle, silver sand dunes)
     - 🏔️ *Starlit Alpine Meadow* (Juniper the mountain goat, high altitude springs)
     - 🪵 *Cozy Hearth & Cabin* (Biscuit the golden cat, crackling stove, snowfall)
     - 🌌 *Hilltop Stargazer* (Sage the quiet owl, constellations, twilight grass)
     - 🍵 *Rainy Bamboo Garden* (Bramble the hedgehog, stone lanterns, gentle rain)
   - Built a progressive wind-down algorithm: initial paragraphs set vivid grounding details, while subsequent paragraphs deliberately shorten sentence structures, introduce progressive muscle relaxation cues, and slow cadence toward sleep.

2. **Procedural Web Audio Engine (Zero External Audio Files)**:
   - Rather than bundling megabytes of MP3 files, the audio engine synthesizes infinite ambient audio in real time using the **Web Audio API**:
     - **Rain**: White noise fed into cascaded highpass (850Hz) and lowpass (6000Hz) biquad filters.
     - **Ocean Waves**: Brown noise modulated by an ultra-slow 0.07Hz sine LFO simulating a 14-second rhythmic wave swell and receding tide.
     - **Night Breeze**: Bandpass-filtered pink noise swept with gentle organic frequency variation.
     - **Campfire**: Lowpass-filtered brown noise rumble coupled with procedural transient burst micro-crackles.
     - **Summer Crickets**: Dual tuned sine oscillators (4250Hz - 4400Hz) pulsed in natural clusters.
     - **Celestial Drone**: 108Hz + 114Hz tuned sine drone creating a therapeutic 6Hz theta relaxation beat combined with sub-bass warmth.

3. **Device Speech Synthesis**:
   - Queries `window.speechSynthesis` locally, scans for natural/enhanced voices on the user's operating system, and applies a hypnotic 0.85x reading rate with measured pauses between paragraphs and breathing interludes.

4. **Automated Verification**:
   - Automated browser subagents tested the application inside a real browser environment, verifying audio context initialization, service worker pre-caching, tab switching, and console telemetry with zero errors.

---

## Why Does Open Innovation Matter?

Closed-source wellness platforms treat sleep and relaxation as a recurring monetization channel:
- They require continuous telemetry and network requests, preventing true offline disconnection.
- They wrap basic noise generators and meditation scripts behind expensive paywalls.
- If a cloud server goes down or your internet drops at 11:30 PM, your sleep aid simply stops working.

Open innovation matters because **rest should not be gated behind an internet connection or an API subscription**. 

By building upon open web standards (HTML5, Web Audio API, Web Speech API, Service Workers), Drift demonstrates that modern browsers already contain all the primitive capabilities required to synthesize rich, soothing multi-sensory experiences locally. Open innovation ensures that this tool remains free, private, accessible to anyone on any device, and resilient enough to keep working indefinitely without server maintenance or corporate deprecation.

---

## My Agent Session

This project was developed and validated collaboratively with Google Antigravity. The agent:
- Researched and structured the single-file offline architecture requested in the challenge specification.
- Generated custom vector branding and high-resolution PWA icons.
- Engineered mathematical noise generation algorithms for all 6 Web Audio layers.
- Formulated the calming multi-chapter narrative grammar.
- Ran live browser subagents to validate audio playback, speech utterance queuing, and service worker offline caching.

---

## 🛠️ Local Development & Deployment

### Run Locally
```bash
# Using Python
python -m http.server 8080

# Or using Node
npx serve .
```
Visit `http://localhost:8080` in any modern web browser.

### Deploy to Render
Drift includes a ready-to-use [`render.yaml`](render.yaml) file. Simply connect this repository to Render and deploy as a **Static Site** with zero build configuration.
