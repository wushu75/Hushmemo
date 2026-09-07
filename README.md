# HushMemo Meet

**Local-first, no-bot meeting notes for your browser.**

Most meeting-notes tools send a bot into your call and stream everything to a
cloud service. HushMemo doesn't. It quietly captures the audio already playing
in your meeting tab, transcribes it **on your own machine**, lets you jot rough
notes as the meeting happens, and afterward turns the transcript plus your
jottings into structured notes — a summary, decisions, action items with
owners, and open questions.

Nothing leaves your computer by default. No bot joins the call. No analytics,
no telemetry.

## Why

- **No bot in the room.** HushMemo uses Chrome's tab-audio capture, so there's
  no extra "Notetaker" participant and nothing to explain to the other people
  on the call. The meeting stays audible the whole time.
- **Local-first.** On-device transcription (Whisper via transformers.js) and
  local note generation (Ollama, or a simple built-in heuristic). Transcripts,
  jottings, and notes are stored in your browser's IndexedDB.
- **Yours to keep.** Export any meeting — or everything — as JSON. Delete a
  meeting and it's gone.
- **Free and open.** MIT-licensed, single-developer-friendly, plain JavaScript,
  no build step.

Inspired by the DoodleNote approach to lightweight, personal meeting notes.

## Get started

The extension lives in [`extension/`](./extension). To try it:

1. Open `chrome://extensions`, enable **Developer mode**.
2. **Load unpacked** → select the `extension/` folder.
3. Open a meeting tab, open the HushMemo side panel, press **Start listening**.

Out of the box it runs fully offline with a transcription **stub** and a
**heuristic** note generator, so you can see the whole flow immediately. Plug in
a real local Whisper model and/or a local LLM when you're ready — see the
[extension README](./extension/README.md) for step-by-step configuration and
the full privacy model.

## How it works

```
 meeting tab audio
        │  chrome.tabCapture
        ▼
 service worker ──mints stream id──▶ offscreen document
                                       │  getUserMedia + Web Audio
                                       ├─▶ speakers (stays audible)
                                       └─▶ 16 kHz chunks ─▶ ASR (local)
                                                             │
        your jottings ─────────────────────────────────────┤
                                                             ▼
                                                        IndexedDB
                                                             │
                                          "Generate notes"   ▼
                                     transcript + jottings ─▶ LLM (local/API)
                                                             │
                                                             ▼
                                      summary · decisions · actions · questions
```

The side panel is the UI; the offscreen document is the audio engine; the
service worker brokers between them. See the file map in the
[extension README](./extension/README.md).

## Project layout

```
.
├── extension/          # the loadable Chrome extension (start here)
│   ├── manifest.json
│   ├── background.js
│   ├── offscreen.html / offscreen.js
│   ├── asr.js
│   ├── sidepanel.html / sidepanel.css / sidepanel.js
│   ├── content.js
│   ├── db.js  llm.js  settings.js
│   ├── icons/
│   └── README.md       # load + config + privacy details
├── LICENSE             # MIT
└── README.md           # you are here
```

## Status

Early and intentionally small. The transcription and LLM engines ship as clear,
well-commented stubs with real integration paths documented, so a single
developer can take it from "works offline as a demo" to "real local Whisper +
local LLM" without rearchitecting anything.

## Contributing

Issues and PRs welcome. Keep it simple, keep it local, and never add telemetry.

## License

[MIT](./LICENSE) © The HushMemo Meet Authors.
