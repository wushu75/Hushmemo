# HushMemo Meet — Privacy Policy

_Last updated: 2026-09-07_

HushMemo Meet is a local-first browser extension. It is designed so that your
meetings stay on your computer. This policy explains, in plain terms, what the
extension handles and what (if anything) ever leaves your device.

## The short version

- HushMemo has **no servers**. The developer does not receive, store, or have
  any access to your audio, transcripts, notes, or settings.
- There is **no account, no sign-in, and no analytics or telemetry**.
- By default, the extension makes **no network requests at all**.
- Data leaves your computer **only** if you deliberately turn on a cloud AI
  provider and enter your own API key — and then it goes directly to the
  provider you chose, not to us.

## What the extension handles, and where it stays

| Data | Purpose | Where it lives |
| --- | --- | --- |
| Tab audio from your call | Transcription | Processed in memory on your device; never written to disk as a file and never uploaded by the extension |
| Transcript text | Building your notes | Stored locally in your browser (IndexedDB) |
| Your typed "jottings" | Building your notes | Stored locally in your browser (IndexedDB) |
| Generated notes | The reason you're here | Stored locally in your browser (IndexedDB) |
| Settings (engine choice, model names, optional API key) | Running the extension | Stored locally via `chrome.storage.local` |
| Microphone audio (only if you tick "Also capture my microphone") | Adding your voice to the transcript | Processed in memory on your device; not uploaded by the extension |

All of the above is stored on your own machine and can be exported or deleted by
you at any time from the extension's Library view.

## When something can leave your device

HushMemo can draft notes in three modes. You choose which one:

1. **Heuristic (default)** — runs entirely on your device. No network.
2. **Local model (Ollama)** — your transcript and jottings are sent to a model
   running on your own computer (`http://localhost:11434`). Nothing leaves the
   machine.
3. **Bring your own cloud API key** — if you enter an API key and endpoint
   (for example, OpenAI), the transcript and jottings for the meeting you are
   summarizing are sent **directly from your browser to that provider** so it can
   generate the notes. This only happens when you explicitly choose this mode and
   press Generate. That data is then handled under **the chosen provider's**
   privacy policy. HushMemo has no server in the middle and never receives a copy.

Speech-to-text is always performed on your device. Transcription is never sent to
a cloud service.

## Permissions, and why they exist

- **tabCapture / offscreen** — to capture the audio of the meeting tab from your
  side and transcribe it locally.
- **activeTab** — so you can point the extension at the tab you want to capture.
- **sidePanel** — the extension's user interface.
- **storage** — to keep your meetings, notes, and settings on your device.
- **tabs** — to detect which meeting app a tab is (Meet, Zoom, Teams) and to
  capture the correct tab.
- **Host access to `localhost` / `127.0.0.1`** — only used if you run a local
  model (Ollama).
- **Optional host access to websites** — requested at the moment you enable a
  cloud API endpoint, so the extension can reach the endpoint you configured.
  Not requested otherwise.

## Children

HushMemo is a general-purpose productivity tool and is not directed at children.

## Changes

If this policy changes, the updated version will be published in the project
repository with a new "Last updated" date.

## Contact

Questions or concerns: please open an issue at
<https://github.com/wushu75/Hushmemo/issues>.
