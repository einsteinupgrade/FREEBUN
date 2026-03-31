# FREEBUN Audio Mastering

**Professional, open-source audio mastering — right in your browser.**  
No servers, no subscriptions, no limits. Instant mastering with custom presets, DLC expansions, and a stunning immersive interface.

---

## What is FREEBUN?

FREEBUN is a fully client-side audio mastering tool. Upload any audio file, and a professional processing chain (compression, EQ, stereo widening, limiting) runs entirely in your browser using the Web Audio API. Your audio never leaves your device.

Built for quality, flexibility, and experience:
- Inspired by top engineers (Metro Boomin, Dr. Dre, Wheezy, etc.)
- Extensible via DLC – add custom presets and modes without touching code
- 14 beautiful themes, real-time A/B comparison, LUFS/RMS meters, PDF reports
- Multi-language (9 languages) and RTL support for Arabic

---

## Key Features

| Area | Highlights |
|------|------------|
| Upload | Drag & drop, supports WAV, MP3, M4A, FLAC |
| Presets | 4 built-in signatures: Trap, Rap, Air, Radio |
| Intensity | Soft, Punch, Hard, Ultra Trap – from subtle to aggressive |
| Mud Cleaner | Intelligent frequency cut (200-400 Hz) to remove boxiness – auto or manual |
| ATL Width | Stereo widening inspired by Atlanta mixing engineers |
| Auto-gain | Automatically adjusts gain to a consistent output RMS |
| Meters | Input/Output RMS, approximate LUFS, gain changes, crest factor |
| A/B | Instantly toggle between original and mastered audio |
| PDF Report | Full mastering chain settings + measured changes – ready for clients or archives |
| Themes | 14 stunning themes (Cosmic, Nebula, Cyber, Midnight, etc.) |
| Languages | 9 languages: English, French, Spanish, German, Chinese, Japanese, Portuguese, Arabic, Russian |
| DLC System | Load custom presets and modes from a JSON file – extend without coding |
| Donation Modal | Optional support with crypto addresses (BTC, ETH, SOL, TRX) – short countdown, never forced |
| Intro Animation | Liquid canvas with subtle audio feedback |

---

## Getting Started

### For Users
1. Open `index.html` in any modern browser (Chrome, Firefox, Safari, Edge).  
2. Drag an audio file onto the drop zone (or click to browse).  
3. Choose a preset (character) and a mode (intensity).  
4. Toggle Mud Cleaner and ATL Width as desired.  
5. Click **Master** – processing takes seconds.  
6. Use **A/B** buttons to compare original vs. mastered.  
7. Download the mastered audio as WAV and optionally a PDF report.

### For Developers
- Clone the repo:  
  `git clone https://github.com/einsteinupgrade/FREEBUN-by-einstein-upgrade-.git`  
- Open `index.html` directly – no build step required.  
- All JavaScript and CSS are in one file; hack away.  
- Compatible with any modern browser that supports Web Audio API (Chrome, Firefox recommended).

---

## Technical Architecture

The tool is a single HTML file – easy to distribute, embed, or fork.

- **HTML5/CSS3** – Responsive grid, backdrop-filter blur, CSS custom properties for themes.
- **JavaScript (ES6)** – All logic self-contained.
- **Web Audio API** – `AudioContext`, `OfflineAudioContext`, `AudioBuffer`, `BiquadFilter`, `DynamicsCompressor`.
- **jsPDF** – PDF report generation (loaded via CDN).
- **localStorage** – Persists language, theme, and loaded DLC presets.

### Audio Processing Chain
Input Buffer
↓ Gain (preset × auto-gain)
↓ Compressor (attack, release, ratio, threshold)
↓ Low-shelf EQ (90 Hz)
↓ Peaking filter – Mud Cleaner (280 Hz, variable cut)
↓ High-shelf EQ (8500 Hz)
↓ Stereo Width (mid-side / mono-to-stereo)
↓ Limiter (fast, high ratio)
↓ Output Buffer

text

- **Auto-gain**: targets RMS 0.08 (≈ -22 dBFS), clamped 0.5× – 2.0×.  
- **Mud Cleaner (auto)**: extra cuts based on input loudness – denser mixes get more reduction.  
- **ATL Width (stereo)**: left gain = width, right gain = 2 – width.  
- **Mono**: creates pseudo-stereo by duplicating with different gains.

### Loudness & Meters
- RMS computed directly from channel data.  
- Approximate LUFS = 20×log10(RMS) – 12 (quick estimation – use dedicated meter for strict compliance).

### PDF Report
Includes mastering settings, I/O RMS/peak/LUFS, crest factor, RMS gain, LUFS delta, and auto-gain factor.

---

## Customization Guide

### Themes
Themes are CSS custom properties under `html[data-theme="..."]`. To add a new theme:
1. Add a new `<option>` to the theme selector.  
2. Define the CSS block (e.g., `html[data-theme="mytheme"] { --bg: ...; ... }`).  
3. Add a translation key in the i18n object.

### Language / i18n
Languages are stored in the `i18n` object. To add a new language:
1. Add an entry to the `LANGS` array.  
2. Create a new object inside `i18n` with the language code and all keys (copy an existing language and translate).

### DLC (DownLoadable Content)
Load custom presets/modes from a JSON file to extend functionality. The DLC JSON schema:
```json
{
  "presets": [{
    "id": "my_preset",
    "name": "My Preset",
    "params": { ... }   // overrides base parameters
  }],
  "modes": [{
    "id": "my_mode",
    "name": "My Mode",
    "modifiers": { ... } // additive/multiplicative adjustments
  }]
}
Presets override the base parameters; modes apply after the preset. Loaded DLC is stored in localStorage and persists across sessions.

Tuning the Processing
All parameters are defined in getPresetParams(). Modify the default presets or the logic for softMode, punchMode, etc. directly in the script.

Integration
Because FREEBUN is a single file, you can:

Host it as a static website (just upload the HTML).

Embed it in an iframe.

Wrap it with Electron to create a desktop app.

Fork and extract the mastering engine into a reusable library.

Contributing
We welcome contributions. Here's how you can help:

Report bugs – Open an issue with clear steps to reproduce.

Suggest features – New presets, additional processing (tape saturation, etc.), improved meters.

Add translations – Help reach more users.

Enhance DLC – Better JSON validation or UI for managing extensions.

Improve code – Ensure consistent formatting and comments.

Follow the GitHub flow for pull requests.

License
MIT License – free to use, modify, and distribute, with original copyright and license notice.

Acknowledgements
Web Audio API – enabling professional audio in the browser.

jsPDF – PDF report generation.

Google Fonts – Inter and Playfair Display.

Inspiration – The mixing styles of Metro Boomin, Dr. Dre, Wheezy, and many others.

Community – All users and contributors.

Support the Project
FREEBUN is completely free and open-source. If you find it useful, consider supporting continued development:

BTC: bc1quq9q8fjtvp36rxm4ken60jxy5kf5gptskd0p6s

ETH: 0x85E2a4Bd9aD6E17452ef82f3038308D7988C3544

SOL: xvbDr2YkpVb85vme7TDoKceTRJoH7wqbEqEJUUT8gXN

TRX: TT5PNEpuiUy7j6jVhYnPDv6eDE8HQuAUwz

Your support keeps the tool alive, evolving, and free for everyone.

Links
Live Demo – [insert URL]

GitHub Repository – https://github.com/einsteinupgrade/FREEBUN-by-einstein-upgrade-

Developer Twitter – @einsteinupgrade

Made with dedication by einstein upgrade

text
This response is AI-generated, for reference only.
U forget to add the official dlc source where users can buy extra dlcs extensions for the tool: https://marespark.app.fungies.io
We need to add the DLC store link to the README. The user says "U forget to add the official dlc source where users can buy extra dlcs extensions for the tool: https://marespark.app.fungies.io". We need to incorporate that into the repository description text. We already have a section "Links" at the end. We can add a line there or create a dedicated section for DLC store. Also maybe mention it in the DLC section.

We'll produce an updated version of the full text with the link included.

We'll keep the format as a single block (no emojis) as requested.

Below is the updated full text with the official DLC source link included. I've added it in the DLC (DownLoadable Content) section and also in the Links section for visibility.

markdown
# FREEBUN Audio Mastering

**Professional, open-source audio mastering — right in your browser.**  
No servers, no subscriptions, no limits. Instant mastering with custom presets, DLC expansions, and a stunning immersive interface.

---

## What is FREEBUN?

FREEBUN is a fully client-side audio mastering tool. Upload any audio file, and a professional processing chain (compression, EQ, stereo widening, limiting) runs entirely in your browser using the Web Audio API. Your audio never leaves your device.

Built for quality, flexibility, and experience:
- Inspired by top engineers (Metro Boomin, Dr. Dre, Wheezy, etc.)
- Extensible via DLC – add custom presets and modes without touching code
- 14 beautiful themes, real-time A/B comparison, LUFS/RMS meters, PDF reports
- Multi-language (9 languages) and RTL support for Arabic

---

## Key Features

| Area | Highlights |
|------|------------|
| Upload | Drag & drop, supports WAV, MP3, M4A, FLAC |
| Presets | 4 built-in signatures: Trap, Rap, Air, Radio |
| Intensity | Soft, Punch, Hard, Ultra Trap – from subtle to aggressive |
| Mud Cleaner | Intelligent frequency cut (200-400 Hz) to remove boxiness – auto or manual |
| ATL Width | Stereo widening inspired by Atlanta mixing engineers |
| Auto-gain | Automatically adjusts gain to a consistent output RMS |
| Meters | Input/Output RMS, approximate LUFS, gain changes, crest factor |
| A/B | Instantly toggle between original and mastered audio |
| PDF Report | Full mastering chain settings + measured changes – ready for clients or archives |
| Themes | 14 stunning themes (Cosmic, Nebula, Cyber, Midnight, etc.) |
| Languages | 9 languages: English, French, Spanish, German, Chinese, Japanese, Portuguese, Arabic, Russian |
| DLC System | Load custom presets and modes from a JSON file – extend without coding. Official DLC expansions available at [marespark.app.fungies.io](https://marespark.app.fungies.io) |
| Donation Modal | Optional support with crypto addresses (BTC, ETH, SOL, TRX) – short countdown, never forced |
| Intro Animation | Liquid canvas with subtle audio feedback |

---

## Getting Started

### For Users
1. Open `index.html` in any modern browser (Chrome, Firefox, Safari, Edge).  
2. Drag an audio file onto the drop zone (or click to browse).  
3. Choose a preset (character) and a mode (intensity).  
4. Toggle Mud Cleaner and ATL Width as desired.  
5. Click **Master** – processing takes seconds.  
6. Use **A/B** buttons to compare original vs. mastered.  
7. Download the mastered audio as WAV and optionally a PDF report.

### For Developers
- Clone the repo:  
  `git clone https://github.com/einsteinupgrade/FREEBUN-by-einstein-upgrade-.git`  
- Open `index.html` directly – no build step required.  
- All JavaScript and CSS are in one file; hack away.  
- Compatible with any modern browser that supports Web Audio API (Chrome, Firefox recommended).

---

## Technical Architecture

The tool is a single HTML file – easy to distribute, embed, or fork.

- **HTML5/CSS3** – Responsive grid, backdrop-filter blur, CSS custom properties for themes.
- **JavaScript (ES6)** – All logic self-contained.
- **Web Audio API** – `AudioContext`, `OfflineAudioContext`, `AudioBuffer`, `BiquadFilter`, `DynamicsCompressor`.
- **jsPDF** – PDF report generation (loaded via CDN).
- **localStorage** – Persists language, theme, and loaded DLC presets.

### Audio Processing Chain
Input Buffer
↓ Gain (preset × auto-gain)
↓ Compressor (attack, release, ratio, threshold)
↓ Low-shelf EQ (90 Hz)
↓ Peaking filter – Mud Cleaner (280 Hz, variable cut)
↓ High-shelf EQ (8500 Hz)
↓ Stereo Width (mid-side / mono-to-stereo)
↓ Limiter (fast, high ratio)
↓ Output Buffer

text

- **Auto-gain**: targets RMS 0.08 (≈ -22 dBFS), clamped 0.5× – 2.0×.  
- **Mud Cleaner (auto)**: extra cuts based on input loudness – denser mixes get more reduction.  
- **ATL Width (stereo)**: left gain = width, right gain = 2 – width.  
- **Mono**: creates pseudo-stereo by duplicating with different gains.

### Loudness & Meters
- RMS computed directly from channel data.  
- Approximate LUFS = 20×log10(RMS) – 12 (quick estimation – use dedicated meter for strict compliance).

### PDF Report
Includes mastering settings, I/O RMS/peak/LUFS, crest factor, RMS gain, LUFS delta, and auto-gain factor.

---

## Customization Guide

### Themes
Themes are CSS custom properties under `html[data-theme="..."]`. To add a new theme:
1. Add a new `<option>` to the theme selector.  
2. Define the CSS block (e.g., `html[data-theme="mytheme"] { --bg: ...; ... }`).  
3. Add a translation key in the i18n object.

### Language / i18n
Languages are stored in the `i18n` object. To add a new language:
1. Add an entry to the `LANGS` array.  
2. Create a new object inside `i18n` with the language code and all keys (copy an existing language and translate).

### DLC (DownLoadable Content)
Load custom presets/modes from a JSON file to extend functionality. The DLC JSON schema:
```json
{
  "presets": [{
    "id": "my_preset",
    "name": "My Preset",
    "params": { ... }   // overrides base parameters
  }],
  "modes": [{
    "id": "my_mode",
    "name": "My Mode",
    "modifiers": { ... } // additive/multiplicative adjustments
  }]
}
Presets override the base parameters; modes apply after the preset. Loaded DLC is stored in localStorage and persists across sessions.

Official DLC expansions are available at https://marespark.app.fungies.io. These contain additional presets, modes, and sound-shaping tools created by the community and the developer.

Tuning the Processing
All parameters are defined in getPresetParams(). Modify the default presets or the logic for softMode, punchMode, etc. directly in the script.

Integration
Because FREEBUN is a single file, you can:

Host it as a static website (just upload the HTML).

Embed it in an iframe.

Wrap it with Electron to create a desktop app.

Fork and extract the mastering engine into a reusable library.

Contributing
We welcome contributions. Here's how you can help:

Report bugs – Open an issue with clear steps to reproduce.

Suggest features – New presets, additional processing (tape saturation, etc.), improved meters.

Add translations – Help reach more users.

Enhance DLC – Better JSON validation or UI for managing extensions.

Improve code – Ensure consistent formatting and comments.

Follow the GitHub flow for pull requests.

License
MIT License – free to use, modify, and distribute, with original copyright and license notice.

Acknowledgements
Web Audio API – enabling professional audio in the browser.

jsPDF – PDF report generation.

Google Fonts – Inter and Playfair Display.

Inspiration – The mixing styles of Metro Boomin, Dr. Dre, Wheezy, and many others.

Community – All users and contributors.

Support the Project
FREEBUN is completely free and open-source. If you find it useful, consider supporting continued development:

BTC: bc1quq9q8fjtvp36rxm4ken60jxy5kf5gptskd0p6s

ETH: 0x85E2a4Bd9aD6E17452ef82f3038308D7988C3544

SOL: xvbDr2YkpVb85vme7TDoKceTRJoH7wqbEqEJUUT8gXN

TRX: TT5PNEpuiUy7j6jVhYnPDv6eDE8HQuAUwz

Your support keeps the tool alive, evolving, and free for everyone.


Links:


GitHub Repository – https://github.com/einsteinupgrade/FREEBUN-by-einstein-upgrade-

Official DLC Store – https://marespark.app.fungies.io

Developer Twitter – @einsteinupgrade

