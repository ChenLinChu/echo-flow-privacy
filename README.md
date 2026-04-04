---
title: EchoFlow Privacy Policy
description: Privacy policy for the EchoFlow Chrome extension (language shadowing on YouTube).
---

# EchoFlow Privacy Policy

**Last updated:** April 4, 2026  

This Privacy Policy describes how **EchoFlow** (“we”, “us”, or “the extension”) handles information when you use our Chrome extension. EchoFlow helps you practice language shadowing on **YouTube** using captions, playback controls, optional recording for self-review, and related features.

By using EchoFlow, you agree to this policy. If you do not agree, please uninstall the extension and discontinue use.

---

## 1. Who we are

EchoFlow is developed by **Chen Lin Chu**.  

**Contact:** [chenlinchu637@gmail.com](mailto:chenlinchu637@gmail.com)

For privacy-related questions, data requests, or concerns, email us at the address above.

---

## 2. Summary (statements also shown in the extension popup)

The following reflects key messages displayed in the extension’s toolbar popup. **Section 3** below provides a fuller technical description so nothing important is omitted.

| Topic | Text shown in the popup (English) |
|--------|-----------------------------------|
| **Product name** | **EchoFlow** |
| **Short description** | Language shadowing practice on YouTube |
| **Pricing notice** | Free for now; advanced paid features may be added later. |
| **Privacy summary** | This extension only collects click and interaction analytics events. It does not collect recording-related personal audio or voice data. |
| **Copyright** | Copyright © Chen Lin Chu. All rights reserved. |
| **Contact** | Use **Contact us** in the popup to open an email to **chenlinchu637@gmail.com**. |

**Clarification of the privacy summary:** We do **not** upload your microphone recordings or voice audio to EchoFlow’s own servers. Optional **Google Analytics** (when enabled in the build you install) sends **usage events** and related metadata (see below). When you use **word translation** or **dictionary lookups**, **words** are sent to third-party APIs as described in Section 3. That detail goes beyond the short popup line but is part of honest disclosure.

---

## 3. Information the extension processes

### 3.1 Locally on your device

- **User settings** (e.g. interface language, subtitle display preferences) are stored with Chrome’s **`chrome.storage.local`** API on your device.
- **Shadowing session state** (e.g. current practice context) may be held in memory during use; it is not uploaded to our servers by EchoFlow.
- **Microphone audio** is accessed only when you start shadowing/recording, through the browser’s standard APIs (**`getUserMedia`**, **`MediaRecorder`**). Recordings are used **locally** in your browser for playback comparison and feedback. EchoFlow **does not** transmit your raw audio recordings to servers we operate.
- **Speech recognition** (where supported by the browser) may be provided by the **browser or operating system**; any cloud processing is governed by **Google Chrome** / your platform provider, not by EchoFlow’s code.

### 3.2 YouTube pages (website content you already see)

- The extension runs only on **`https://www.youtube.com/*`** as declared in the manifest.
- It reads **caption / timedtext** data needed to show subtitle lines and sync practice. That text is **video content** available on the page or through YouTube’s normal caption mechanisms while you watch.

### 3.3 Analytics (optional)

If the distributed build includes a **Google Analytics 4** Measurement ID, the extension may send events to **Google** (`https://www.google-analytics.com`), for example:

- Interaction-related event names (e.g. starting practice, using controls).
- **Page URL** (`document.location`) of the page where the event occurred (typically a YouTube watch URL).
- For some events, parameters such as **video title** (truncated where applicable) when you start practice.
- A **pseudonymous client identifier** stored in `chrome.storage.local` to distinguish installations without logging in.

Analytics is intended for **product improvement**, not for selling personal data. You can learn how Google uses data in Google’s privacy documentation.

### 3.4 Translation (when you tap a word)

If you use **click-to-translate**, the **selected word or short phrase** and language metadata are sent to the **MyMemory Translation API** (`api.mymemory.translated.net`) to retrieve machine translations. This happens **only when you trigger** that feature. See MyMemory’s terms and privacy policy for their handling of requests.

### 3.5 Dictionary / phonetics (English words)

To show **IPA / KK-style phonetics** for English words appearing in subtitles, the extension may request public dictionary data from the **Free Dictionary API** (`api.dictionaryapi.dev`). Only **word text** needed for lookup is sent.

---

## 4. Legal bases and purposes (EEA / UK users — general information)

Depending on your region, processing may rely on **consent** (e.g. microphone when you start recording), **contract / user request** (providing the extension’s features), or **legitimate interests** (limited analytics to improve stability and features). This statement is informational; consult applicable law for your situation.

---

## 5. Third-party services

| Service | Purpose | Typical data involved |
|---------|---------|------------------------|
| **Google / YouTube** | Site where the extension runs | Pages and content you view there (under YouTube’s policies) |
| **Google Analytics** | Optional usage statistics | Events, URLs, optional titles, client id |
| **MyMemory** | Optional word translation | Word/phrase, language pair |
| **Free Dictionary API** | English phonetic lookup | English word |

We do not control these third parties’ policies; please read their documentation.

---

## 6. Data retention

- **Local storage** on your device persists until you clear extension data or uninstall Chrome (or the extension), subject to Chrome’s behavior.
- **Analytics** retention is governed by your **Google Analytics** property settings (configured by the publisher of the build you use).
- EchoFlow does **not** operate a user account database for end users.

---

## 7. Sale of data; unrelated uses

We **do not sell** your personal information. We **do not** use data for **creditworthiness or lending**. We use data only to provide and improve EchoFlow and as described here.

---

## 8. Security

We design the extension to minimize data collection. No security practice is perfect; use EchoFlow at your own risk on networks and devices you trust.

---

## 9. Children’s privacy

EchoFlow is not directed at children under 13 (or the minimum age in your jurisdiction). If you believe we have inadvertently collected information from a child, contact us and we will work with you to address it.

---

## 10. International users

If you use EchoFlow from outside your home country, data may be processed in countries where Google or other providers operate, subject to their policies.

---

## 11. Changes to this policy

We may update this Privacy Policy. The **“Last updated”** date at the top will change when we do. Continued use after changes means you accept the updated policy. For material changes, we may also note them in the Chrome Web Store listing or extension popup where practical.

---

## 12. Your rights

Depending on where you live, you may have rights to **access**, **correct**, **delete**, or **object** to certain processing, or to **lodge a complaint** with a supervisory authority. Because EchoFlow does not maintain traditional user accounts, many requests can be satisfied by **clearing extension storage**, **resetting the client id** (if present), or **uninstalling** the extension. For other requests, contact us at **chenlinchu637@gmail.com**.

---

## 13. Open source / repository

If this policy is hosted from the project repository (e.g. GitHub Pages), the same document may be available at the repository URL. The **Chrome Web Store** listing should link to the **canonical** policy URL you provide to Google.

---

## 14. Copyright

**Copyright © Chen Lin Chu. All rights reserved.**

EchoFlow, its name, branding, and original code are owned by Chen Lin Chu unless otherwise stated. Third-party trademarks (e.g. YouTube, Google) belong to their respective owners.

---

### Publishing this file on GitHub Pages

- Ensure **GitHub Pages** is enabled for this repository (e.g. branch `main`, folder `/ (root)` or `/docs` depending on your setup).
- If you use **Jekyll** (default for GitHub Pages), this file’s YAML front matter helps set the page title.
- After deployment, use the public HTTPS URL of this page (e.g. `https://<user>.github.io/<repo>/privacy.html` or your custom domain) as the **Privacy policy URL** in the Chrome Web Store Developer Dashboard.

If your Pages setup serves Markdown as `.md`, confirm the final public URL is stable and readable **without signing in** to GitHub.