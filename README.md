---
title: EchoFlow Privacy Policy
description: Privacy policy for the EchoFlow Chrome extension (language shadowing on YouTube).
---

# EchoFlow Privacy Policy

**Last updated:** April 5, 2026

This Privacy Policy describes how **EchoFlow** (“we”, “us”, or “the extension”) handles information
when you use our Chrome extension. EchoFlow helps you practice language shadowing on **YouTube**
using captions, playback controls, optional recording for self-review, and related features.

By using EchoFlow, you agree to this policy. If you do not agree, please uninstall the extension and
discontinue use.

---

## 1. Who we are

EchoFlow is developed by **EchoFlow**.

**Contact:** [echoflow.support@gmail.com](mailto:echoflow.support@gmail.com)

For privacy-related questions, data requests, or concerns, email us at the address above.

---

## 2. Summary (statements also shown in the extension popup)

The following reflects key messages displayed in the extension’s toolbar popup. **Section 3** below
provides a fuller technical description so nothing important is omitted.

| Topic                                | Text shown in the popup (English)                                                                                                                                                  |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Product name**                     | **EchoFlow**                                                                                                                                                                       |
| **Short description**                | Language shadowing practice on YouTube                                                                                                                                             |
| **Pricing notice**                   | Free for now; advanced paid features may be added later.                                                                                                                           |
| **Privacy summary**                  | This extension only collects click and interaction analytics events. It does not collect recording-related personal audio or voice data.                                           |
| **Pronunciation (TTS)**              | When the video is paused, tapping a word may play its pronunciation using Chrome’s built-in text-to-speech. The voice depends on your system and installed speech engines.         |
| **Copyright**                        | Copyright © EchoFlow. All rights reserved.                                                                                                                                         |
| **Third-party content (Wiktionary)** | The popup and shadowing panel link to **English Wiktionary** and the **CC BY-SA 4.0** license deed, and state that phonetic data is community-authored (see each entry’s history). |
| **Contact**                          | Use **Contact us** in the popup (above the legal notices) to open an email to **echoflow.support@gmail.com**.                                                                      |

**Clarification of the privacy summary:** We do **not** upload your microphone recordings or voice
audio to EchoFlow’s own servers. Optional **Google Analytics** (when enabled in the build you
install) sends **usage events** and related metadata (see below). When you use **word translation**,
**pronunciation playback**, or **dictionary lookups**, **words** may be sent to third-party APIs or
processed by your browser as described in Section 3. That detail goes beyond the short popup line
but is part of honest disclosure.

---

## 3. Information the extension processes

### 3.1 Locally on your device

- **User settings** (e.g. interface language, subtitle display preferences, whether the on-page
  shadowing controls are enabled) are stored with Chrome’s **`chrome.storage.local`** API on your
  device.
- **Ephemeral phonetics cache** (dictionary IPA lookups fetched from Wiktionary during a browser
  session) may be stored in **`chrome.storage.session`** so lookups can survive brief extension
  service worker restarts; it is cleared when the browser session ends and is not sent to EchoFlow
  servers.
- **Shadowing session state** (e.g. current practice context) may be held in memory during use; it
  is not uploaded to our servers by EchoFlow.
- **Microphone audio** is accessed only when you start shadowing/recording, through the browser’s
  standard APIs (**`getUserMedia`**, **`MediaRecorder`**). Recordings are used **locally** in your
  browser for playback comparison and feedback. EchoFlow **does not** transmit your raw audio
  recordings to servers we operate.
- **Speech recognition** runs **locally in your browser** using **Transformers.js** and an **OpenAI
  Whisper**-compatible model (default **Base**; you may choose **Small** in settings for higher
  accuracy). The extension **downloads model weights** from **Hugging Face** (`huggingface.co`),
  from the public repositories **`onnx-community/whisper-base.en`** (default) and optionally
  **`onnx-community/whisper-small.en`**. ONNX WASM loaders are served from the extension package.
  Audio is **not** sent to EchoFlow’s servers for transcription; processing stays on your device
  (GPU via **WebGPU** when available, otherwise CPU/WASM).
- The Whisper model is loaded when you **start shadowing** (after you choose to practice), not
  automatically in the background before that. Optional **live** transcription during recording is
  **off by default** in the current build; a full pass still runs **on your device** when a take
  ends (same Hugging Face model files as above; **no** upload of your microphone audio).

### 3.2 YouTube pages (website content you already see)

- The extension runs only on **`https://www.youtube.com/*`** as declared in the manifest.
- It reads **caption / timedtext** data needed to show subtitle lines and sync practice. That text
  is **video content** available on the page or through YouTube’s normal caption mechanisms while
  you watch.

#### Timedtext bridge, `postMessage`, and same-page scripts

To read captions that the player loads with your session cookies, EchoFlow injects a small script
(**`timedtext-bridge.js`**) into the page’s **main JavaScript world** (not the extension’s isolated
world). That script intercepts YouTube’s own timedtext responses, keeps a **bounded in-memory
cache**, and exchanges messages with the extension via **`window.postMessage`**, targeted at this
tab’s **origin** (e.g. `https://www.youtube.com`).

**Same-origin scripts on the watch page** (including other browser extensions that inject into the
page, or scripts on the site) could **listen for** those messages or **send** the same message
types. In particular, another script running in this tab could request the **latest cached timedtext
payload** the bridge holds (similar to what the extension does to show subtitles). This does **not**
send your captions to EchoFlow’s servers; it is a **same-tab, same-origin** interaction. If you use
other extensions or user scripts on YouTube, their behavior is outside EchoFlow’s control.

### 3.3 Analytics (optional)

If the distributed build includes a **Google Analytics 4** Measurement ID, the extension may send
events to **Google** (`https://www.google-analytics.com`), for example:

- Interaction-related event names (e.g. starting practice, using controls).
- **Page URL** metadata: each hit may include the Measurement Protocol **`dl` (document location)**
  parameter set to the tab’s full **`location.href`** (e.g. a YouTube watch URL **with** list or
  timestamp query parameters when present). Separately, the `start_practice` event also sends a
  **canonical watch URL** (`https://www.youtube.com/watch?v=<video id>`) **without** those tracking
  or incidental query parameters in a dedicated event parameter.
- For some events, parameters such as **video title** (truncated where applicable) when you start
  practice.
- When you change settings, a **`settings_change`** event may include the **setting key** and a
  **string form of the new value** (length-capped in the client).
- When you use **click-to-translate** or **tap-to-pronounce**, optional analytics events such as
  **`word_translate_request`** and **`word_pronunciation_play`** may record **UI source** metadata
  (e.g. cue vs. feedback region). They are **not** intended to carry full subtitle sentences.
- After a shadowing comparison, when a word is marked as a mismatch, **the reference word and the
  recognized spoken word** (each truncated) may be sent as event parameters for product improvement.
- A **pseudonymous client identifier** and **session counters** (`sid` / `sct`-style fields) stored
  or derived in `chrome.storage.local` to approximate GA4 sessions without logging in.

Analytics is intended for **product improvement**, not for selling personal data. You can learn how
Google uses data in Google’s privacy documentation.

### 3.4 Translation (when you tap a word)

If you use **click-to-translate**, the **selected word or short phrase** and language metadata are
sent to the **MyMemory Translation API** (`api.mymemory.translated.net`) to retrieve machine
translations. The HTTP request is issued **from the extension** while you are on YouTube (declared
`host_permissions` in the manifest). This happens **only when you trigger** that feature. See
MyMemory’s terms and privacy policy for their handling of requests.

With the same gesture, the extension may **read the word aloud** using **Chrome’s built-in
text-to-speech** (`chrome.tts`) from the extension’s background context. The **word text** is sent
to your **browser / operating system speech engine** (not to EchoFlow’s servers). Available voices
and whether synthesis runs offline depend on your **Chrome version and OS**.

### 3.5 Phonetics (English words, Wiktionary)

To show **IPA / KK-style phonetics** for English words appearing in subtitles, the extension may
request public **Wiktionary** pages via the **MediaWiki Action API** on `en.wiktionary.org` (parsed
HTML for the word’s entry). Only **word text** needed for lookup is sent in the request URL. To
prefetch neighboring lines, the **extension background** may receive a **bounded-length lookup
string** derived from subtitle text over an internal message; outbound **Wiktionary** requests still
use **per-word** page titles in the URL, not the full sentence as a single title.

---

## 4. Legal bases and purposes (EEA / UK users — general information)

Depending on your region, processing may rely on **consent** (e.g. microphone when you start
recording), **contract / user request** (providing the extension’s features), or **legitimate
interests** (limited analytics to improve stability and features). This statement is informational;
consult applicable law for your situation.

---

## 5. Third-party services

| Service                    | Purpose                                                          | Typical data involved                                       |
| -------------------------- | ---------------------------------------------------------------- | ----------------------------------------------------------- |
| **Google / YouTube**       | Site where the extension runs                                    | Pages and content you view there (under YouTube’s policies) |
| **Google Analytics**       | Optional usage statistics                                        | Events, URLs, optional titles, client id                    |
| **Hugging Face**           | Downloading Whisper ONNX weights (`onnx-community/whisper-*.en`) | Model files; **not** your microphone audio (see §3.1)       |
| **MyMemory**               | Optional word translation                                        | Word/phrase, language pair                                  |
| **Chrome / OS TTS**        | Optional tap-to-pronounce                                        | Word text processed by browser/OS speech engine             |
| **Wiktionary (Wikimedia)** | English phonetic lookup (parsed entry HTML)                      | English word (in API URL)                                   |

We do not control these third parties’ policies; please read their documentation.

---

## 6. Data retention

- **Local storage** on your device persists until you clear extension data or uninstall Chrome (or
  the extension), subject to Chrome’s behavior.
- **Analytics** retention is governed by your **Google Analytics** property settings (configured by
  the publisher of the build you use).
- EchoFlow does **not** operate a user account database for end users.

---

## 7. Sale of data; unrelated uses

We **do not sell** your personal information. We **do not** use data for **creditworthiness or
lending**. We use data only to provide and improve EchoFlow and as described here.

---

## 8. Security

We design the extension to minimize data collection. No security practice is perfect; use EchoFlow
at your own risk on networks and devices you trust.

The timedtext bridge only performs **credentialed fetches** to **YouTube-family caption URLs** that
include `timedtext` in the path or query; it is not intended as a general-purpose proxy. For more
context on `postMessage` and same-page scripts, see **Timedtext bridge, `postMessage`, and same-page
scripts** under Section 3.2 above.

---

## 9. Children’s privacy

EchoFlow is not directed at children under 13 (or the minimum age in your jurisdiction). If you
believe we have inadvertently collected information from a child, contact us and we will work with
you to address it.

---

## 10. International users

If you use EchoFlow from outside your home country, data may be processed in countries where Google
or other providers operate, subject to their policies.

---

## 11. Changes to this policy

We may update this Privacy Policy. The **“Last updated”** date at the top will change when we do.
Continued use after changes means you accept the updated policy. For material changes, we may also
note them in the Chrome Web Store listing or extension popup where practical.

---

## 12. Your rights

Depending on where you live, you may have rights to **access**, **correct**, **delete**, or
**object** to certain processing, or to **lodge a complaint** with a supervisory authority. Because
EchoFlow does not maintain traditional user accounts, many requests can be satisfied by **clearing
extension storage**, **resetting the client id** (if present), or **uninstalling** the extension.
For other requests, contact us at **echoflow.support@gmail.com**.

---

## 13. Open source / repository

If this policy is hosted from the project repository (e.g. GitHub Pages), the same document may be
available at the repository URL. The **Chrome Web Store** listing should link to the **canonical**
policy URL you provide to Google.

---

## 14. Copyright

**Copyright © EchoFlow. All rights reserved.**

EchoFlow, its name, branding, and original code are owned by EchoFlow unless otherwise stated.
Third-party trademarks (e.g. YouTube, Google) belong to their respective owners.

---

### Publishing this file on GitHub Pages

- Ensure **GitHub Pages** is enabled for this repository (e.g. branch `main`, folder `/ (root)` or
  `/docs` depending on your setup).
- If you use **Jekyll** (default for GitHub Pages), this file’s YAML front matter helps set the page
  title.
- After deployment, use the public HTTPS URL of this page (e.g.
  `https://<user>.github.io/<repo>/privacy.html` or your custom domain) as the **Privacy policy
  URL** in the Chrome Web Store Developer Dashboard.

If your Pages setup serves Markdown as `.md`, confirm the final public URL is stable and readable
**without signing in** to GitHub.
