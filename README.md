FREEBUN Audio Mastering

Professional, open‑source audio mastering in your browser
No servers, no subscriptions, no limitations — just instant, high‑quality mastering with custom presets, DLC expansions, and a stunning immersive interface.

https://img.shields.io/badge/License-MIT-yellow.svg
https://img.shields.io/badge/PRs-welcome-brightgreen.svg
https://img.shields.io/badge/Web%20Audio-API-blue

🎧 Overview

FREEBUN is a fully client‑side audio mastering tool that runs entirely in your browser. It applies professional‑grade processing chains (compression, EQ, stereo widening, limiting) to any uploaded audio file and lets you download the mastered result as a WAV file. All processing is done with the Web Audio API and OfflineAudioContext – your audio never leaves your device.

Built with a focus on:

· Quality – Inspired by top engineers (Metro Boomin, Dr. Dre, Wheezy, etc.)
· Flexibility – Multiple presets, modes, and DLC support for custom extensions
· Experience – 14 beautiful themes, real‑time A/B comparison, LUFS/RMS meters, PDF reports
· Accessibility – Multi‑language support (9 languages), RTL layout for Arabic

---

✨ Key Features

· Drag & drop upload – Supports WAV, MP3, M4A, FLAC.
· 4 built‑in presets – Trap Signature, Rap Signature, Air Signature, Radio Signature.
· 4 intensity modes – Soft, Punch, Hard, Ultra Trap.
· “Mud Cleaner” – Intelligent frequency‑specific cut to remove boxiness (auto or manual).
· “ATL Width” – Stereo widening inspired by Atlanta mixing engineers.
· Auto‑gain & loudness management – Automatically adjusts gain to reach a consistent output RMS.
· Real‑time meters – Input/Output RMS, approximate LUFS, gain changes, and crest factor.
· A/B comparison – Instantly toggle between original and mastered audio while playing.
· PDF report – Full mastering chain settings and measured changes, ready for client or archiving.
· 14 stunning themes – Cosmic, Nebula, Supernova, Void, Ocean, Aurora, Sunset, Cyber, Golden, Ice, Lava, Forest, Cherry, Midnight.
· Internationalization – 9 languages (English, French, Spanish, German, Chinese, Japanese, Portuguese, Arabic, Russian).
· DLC system – Load custom presets and modes from a JSON file to extend functionality without code changes.
· Donation modal – Optional support for the project with cryptocurrency addresses (BTC, ETH, SOL, TRX) and a short countdown before download (no forced donation).
· Intro animation – Liquid canvas animation with subtle audio feedback.

---

🚀 Getting Started

For Users

1. Open index.html in any modern browser (Chrome, Firefox, Safari, Edge).
2. Drag an audio file onto the drop zone or click to browse.
3. Select a preset (the character of the master) and a mode (intensity).
4. Toggle Mud Cleaner and ATL Width as desired.
5. Click Master – the processing happens in seconds.
6. Use the A/B buttons to compare original and mastered audio.
7. Download the mastered audio as WAV and optionally a PDF report.

For Developers

1. Clone the repository:
   ```bash
   git clone https://github.com/einsteinupgrade/FREEBUN-by-einstein-upgrade-.git
   cd FREEBUN-by-einstein-upgrade-
   ```
2. Open index.html directly in your browser (no build step required).
3. Hack away – all JavaScript and CSS are inside the single HTML file.

Browser compatibility: Requires a browser that supports Web Audio API (all modern browsers). For best performance, use Chrome or Firefox.

---

🧠 Technical Architecture

The entire application is contained in a single HTML file, making distribution and embedding trivial. The main technologies:

· HTML5 / CSS3 – Responsive grid, backdrop‑filter blur, CSS custom properties (themes).
· JavaScript (ES6) – All logic is self‑contained.
· Web Audio API – AudioContext, OfflineAudioContext, AudioBuffer, BiquadFilter, DynamicsCompressor.
· jsPDF – PDF report generation (loaded via CDN).
· localStorage – Saves language, theme, and loaded DLC presets.

Audio Processing Chain

```
Input Audio Buffer
   ↓
Gain (manual preset gain × auto‑gain)
   ↓
Compressor (attack, release, ratio, threshold)
   ↓
Low‑shelf EQ (90 Hz)
   ↓
Peaking filter – “Mud Cleaner” (adjustable cut at 280 Hz)
   ↓
High‑shelf EQ (8500 Hz)
   ↓
Stereo Width (mid‑side / mono‑to‑stereo using gain per channel)
   ↓
Limiter (fast, high ratio, soft clipping effect)
   ↓
Output Buffer
```

· Auto‑gain calculates a factor to bring the input RMS to a target of 0.08 (≈ –22 dBFS), clamped between 0.5x and 2.0x.
· Mud Cleaner in “auto” mode applies additional cuts based on input loudness – louder, denser mixes get more reduction.
· ATL Width for stereo files: left channel gain = width, right channel gain = 2 – width. For mono files, it creates pseudo‑stereo by duplicating with different gains.

Loudness & Meters

· RMS is computed directly from the channel data.
· Approximate LUFS is derived from RMS: LUFS ≈ 20*log10(RMS) – 12. This is a quick estimation; for strict compliance, use a dedicated loudness meter.

PDF Report

The report includes:

· Mastering settings (preset, mode, mud/width, compressor parameters, EQ values)
· Input/output RMS, peak, LUFS
· Derived metrics: crest factor, RMS gain, LUFS delta, auto‑gain factor

---

🛠 Customization Guide

🎨 Themes

Themes are defined as CSS custom properties in the :root of each html[data-theme="..."] block. To add a new theme:

1. Add a new <option> to the theme <select>.
2. Define a new CSS rule, e.g.:
   ```css
   html[data-theme="mytheme"] {
     --bg: #...;
     --bg2: #...;
     --panel: rgba(...);
     --accent: #...;
     --accent2: #...;
   }
   ```
3. Add a translation for the theme name in i18n objects.

🌐 Language / i18n

Languages are stored in the i18n object. To add a new language:

1. Add an entry to the LANGS array with a language code and name.
2. Create a new object inside i18n with the same code, containing all keys. (You can copy an existing language and translate.)
3. The UI will automatically reflect the new language when selected.

📦 DLC (DownLoadable Content)

FREEBUN supports loading JSON files that define custom presets and modes. This allows you to expand the tool without touching the core code.

DLC JSON Schema

```json
{
  "presets": [
    {
      "id": "my_preset_id",
      "name": "My Custom Preset",
      "params": {
        "gain": 1.1,
        "comp": {
          "threshold": -20,
          "ratio": 5,
          "attack": 0.008,
          "release": 0.12,
          "knee": 12
        },
        "lowShelfGain": 4.0,
        "highShelfGain": 3.0,
        "limiterThr": -2.5,
        "width": 1.04,
        "mudReduction": -1.0
      }
    }
  ],
  "modes": [
    {
      "id": "my_mode_id",
      "name": "My Special Mode",
      "modifiers": {
        "gain": 1.05,
        "compRatio": 1.1,
        "limiterThr": 0.5,
        "mudReduction": -0.5
      }
    }
  ]
}
```

· Presets override the base parameters. Any missing parameters will fall back to the default “trapdefault” preset.
· Modes are applied after the preset. Their modifiers are multiplicative or additive to the current parameters.

Users can load DLC via the “Load Extension” button. The loaded presets and modes are stored in localStorage and persist across sessions.

🔧 Audio Processing Tuning

All processing parameters are defined in getPresetParams(). You can modify the default presets or the logic for “softMode”, “punchMode”, etc. directly in the script.

---

🔌 Integration

Because the tool is a single self‑contained HTML file, it can be:

· Hosted as a static website – Just upload the HTML file to any web server.
· Embedded in an iframe – Use it as part of a larger audio production suite.
· Used as a desktop app – Wrap it with Electron or a similar framework.
· Forked and extended – The code is modular enough to separate the mastering engine into a reusable library (e.g., extract the processMastering function).

To embed, simply include the HTML in your project and ensure all assets (fonts, jsPDF) are reachable. The code automatically initializes the UI.

---

🤝 Contributing

We welcome contributions! Here’s how you can help:

1. Report bugs – Open an issue with a clear description and steps to reproduce.
2. Suggest features – New presets, additional processing modules (e.g., tape saturation), improved meters.
3. Add translations – Help us reach more users by adding a new language.
4. Improve the DLC system – Enhance JSON validation or add UI for managing extensions.
5. Fix code style – Ensure consistent formatting and comments.

Please follow the GitHub flow for pull requests.

Development Tips

· The entire app is in one file – you can use any IDE.
· To test DLC, create a sample JSON file and use the “Load Extension” button.
· For audio processing changes, test with different sample rates and channel counts (mono/stereo).

---

📄 License

This project is open source under the MIT License. You are free to use, modify, and distribute it, provided the original copyright and license notice are included.

---

🙏 Acknowledgements

· Web Audio API – for enabling professional‑grade audio processing in the browser.
· jsPDF – for PDF report generation.
· Google Fonts – Inter and Playfair Display fonts.
· Inspiration – The presets are inspired by the mixing styles of Metro Boomin, Dr. Dre, Wheezy, and many other engineers.
· Community – All users and contributors who support the project.

---

💖 Support the Project

FREEBUN is completely free and open source. If you find it useful, consider supporting continued development:

· BTC: bc1quq9q8fjtvp36rxm4ken60jxy5kf5gptskd0p6s
· ETH: 0x85E2a4Bd9aD6E17452ef82f3038308D7988C3544
· SOL: xvbDr2YkpVb85vme7TDoKceTRJoH7wqbEqEJUUT8gXN
· TRX: TT5PNEpuiUy7j6jVhYnPDv6eDE8HQuAUwz

Your support helps keep the tool alive, evolving, and free for everyone.

---

🔗 Links

· Live Demo – (Include your hosted URL if available)
· GitHub Repository – https://github.com/einsteinupgrade/FREEBUN-by-einstein-upgrade-
· Developer Twitter – @einsteinupgrade

---

Made with 🎧 by einstein upgrade"