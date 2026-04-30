# feedback-scam 🎓

> Because manually clicking "neutral" 200 times is a crime against humanity.

A Playwright-powered automation tool that fills out the BITS Pilani ERP semester feedback forms so you can spend that time doing literally anything else — sleeping, staring at a wall, contemplating your GPA.

---

## What it does

- Connects to your existing Chrome session via CDP (no login needed)
- Finds every pending **Overall Sem Feedback** on the Student Feedback page
- Selects the **neutral/middle option** for every rating question
- Types `.` in every text field (you're welcome, professors)
- Handles multi-instructor forms, saves each course, and moves on
- Does all 16 (or however many you have) in one shot

---

## Requirements

- Node.js (any recent version)
- A Chromium-based browser (Chrome, Brave, Edge)
- A soul tired enough to automate academic bureaucracy

---

## Setup

```bash
git clone https://github.com/priyansh-x/feedback-scam
cd feedback-scam
npm install
```

---

## Usage

**Step 1 — Launch Chrome with remote debugging:**

_macOS_
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --remote-debugging-port=9222 \
  --user-data-dir=/tmp/chrome-feedback
```

_Linux_
```bash
google-chrome --remote-debugging-port=9222 --user-data-dir=/tmp/chrome-feedback
```

_Windows_
```cmd
start chrome --remote-debugging-port=9222 --user-data-dir="%TEMP%\chrome-feedback"
```

> **Note:** Use `/tmp/chrome-feedback` (or any non-default path) — Chrome refuses to enable remote debugging on its default profile for "security reasons", which is ironic given what we're doing.

**Step 2 — Log into the ERP and navigate to:**
`Self Service → Academic Records → Student Feedback`

**Step 3 — Run it:**
```bash
node fill-feedback.js
```

Watch the terminal. It'll tell you exactly what it's filling and when it's done.

---

## Options

Only want to fill some courses? Use the flags:

```bash
node fill-feedback.js --start=3 --count=2
```

| Flag | Description |
|------|-------------|
| `--start=N` | 1-based index of the course to start from (default: 1) |
| `--count=N` | How many courses to fill before stopping (default: all) |

Useful if you partially filled some manually like an animal.

---

## How it picks answers

- **Rating questions** (strongly agree → strongly disagree): always picks the **middle option** (neutral)
- **Attendance questions** (>80% → <20%): picks the **middle bracket**
- **Text fields**: fills `.` — short enough to not matter, long enough to not be empty

---

## Disclaimer

This tool expresses your genuine, deeply considered, neutral opinion about every course you took this semester. The fact that it took 0.3 seconds per question is simply a testament to your decisiveness.

---

## Issues / PRs

It either works or it doesn't. But if it doesn't, open an issue and describe your suffering.
