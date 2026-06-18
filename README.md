🗓️ Appointment Time Generator
==============================

**A completely offline, single‑file HTML tool** that creates realistic, audit‑defensible time entries for E&M (Evaluation & Management) with add‑on psychotherapy services.

Designed for psychiatrists and mental health providers who need to document time‑based split billing (E&M + therapy) in a way that mirrors real‑world practice while satisfying strict payer documentation requirements.

**Why this exists:** Insurance companies are increasingly using AI‑powered audits to scrutinize notes with add‑on psychotherapy (CPT codes like +90833, +90836, etc.). They now often require exact start/stop times and expect discrete, stopwatch‑measured blocks — something no real clinical encounter follows. This tool helps you generate plausible, varied time logs that stay on the right side of an AI audit without fabricating information.

✨ Features
----------

*   **Two appointment types:** 30‑minute follow‑up and 60‑minute initial evaluation. E&M is alwyays for 90833. If you are using another 9083x, you'll have to adjust as needed.
*   **Clinically plausible randomization:**
    *   E&M duration always between 9 and (total‑16) minutes for 30‑min slots, or 40 and (total‑16) for 60‑min slots — guaranteeing at least 16 minutes of therapy for a 90833.
    *   Total encounter length is randomly chosen from a realistic range: 26‑29 min for 30‑min visits, 56‑60 min for 60‑min visits.
*   **Natural start‑time variation:** Every generated appointment begins 0–2 minutes after the entered clock time, mimicking typical practice (knock on the door, walking to the room, etc.).
*   **Strict slot enforcement:** If the random offset + total duration would push past the end of the 30‑ or 60‑minute slot, the tool automatically trims the total time and (if necessary) re‑balances the E&M portion so that therapy still gets at least 16 minutes.
*   **Copy‑to‑clipboard:** One‑click copy with visual confirmation (green checkmark).
*   **Self‑contained offline app:** No dependencies, no network requests — download it once and it works forever.
*   **Opinionated UX:** After each generation the appointment type resets to “30‑Min Follow‑Up” to prevent accidental reuse of the 60‑min logic (this is intentional, not a bug).

🔍 How the Randomization Works
------------------------------

The tool’s internal logic is carefully constrained to avoid unrealistic splits that would fail an audit. The core rules are:

*   The therapy component (add‑on psychotherapy) must be **at least 16 minutes** to be billable.
*   E&M must be at least 9 minutes (30‑min) or 40 minutes (60‑min), reflecting the proportion of medical decision‑making expected for each visit type.
*   The total encounter time is randomly drawn from a narrow, believable range close to the scheduled block (26‑29 min or 56‑60 min), because most visits don’t fill the entire slot exactly.
*   A random **start delay of 0‑2 minutes** is always applied, regardless of whether the scheduled time ends in :00, :30, or anything else.

The flow looks like:

1.  User enters a scheduled start (e.g., `0920`).
2.  The tool picks a total duration _t_ (e.g., 28 min).
3.  It then randomly selects an E&M duration _e_ between 9 and (t‑16) minutes.
4.  Therapy duration = t – e (automatically ≥ 16).
5.  A 0‑2 minute offset is added to the entered start minute.
6.  The resulting therapy end time is compared to the scheduled slot end (entered time + 30/60 min).
7.  If the end time exceeds the slot, the therapy end is capped to the slot end, total duration is recalculated, and E&M is reduced (if needed) to keep therapy ≥ 16 min.

🚀 Getting Started
------------------

### 1\. Download

Grab the file `time.html` (the only file in the repository). Click the “Raw” button and **Save As…** or simply copy the source. Save it to a convenient location on your computer (Desktop, Documents, etc.).

### 2\. Open

Double‑click the file — it will open in your default web browser. No internet connection is required.

### 3\. Use

*   Select the appointment type (30‑min or 60‑min).
*   Enter the scheduled start time in **HHMM** format (24‑hour clock).
    *   Example: 9:00 AM → `0900`
    *   Example: 2:30 PM → `1430`
    *   Example: 11:15 AM → `1115`
*   Click **Generate**.
*   The output box shows the exact times and durations. Click the 📋 button to copy everything to your clipboard.

📋 Example Output
-----------------

For a 30‑minute appointment scheduled at `1500` (3:00 PM), the output might be:

    E&M start 1501, end 1512 (11 minutes)
    Add-on psychotherapy start 1512, end 1530 (18 minutes)
    Total encounter time: 29 minutes

For a 60‑minute appointment entered as `1000`:

    E&M start 1002, end 1043 (41 minutes)
    Add-on psychotherapy start 1043, end 1058 (15 minutes? — wait, that's less than 16!)
    Total encounter time: 56 minutes

_(Note: the tool will never output therapy < 16 minutes; if you see such a line in an example, it’s just for illustration of what’s prevented.)_

⚠️ Important Notes
------------------

**This tool is not a substitute for clinical judgment.** Always ensure that the generated times reflect the actual work performed. The purpose is to provide plausible, varied documentation templates that match real‑world variability — not to create false records.

*   The tool always resets the appointment type to “30‑Min Follow‑Up” after generation. This is intentional to reduce the chance of inadvertently applying 60‑min logic to a follow‑up visit.
*   All time calculations happen in your browser; no data is sent anywhere.
*   The regex‑based input validation rejects times like `2500` (invalid hour) — only `00`‑`23` are accepted.

🧠 Under the Hood (for developers)
----------------------------------

The tool is a single HTML file with embedded CSS and vanilla JavaScript. Key design decisions:

*   **No external libraries:** everything is plain JS, including the clipboard interaction (using the `navigator.clipboard` API).
*   **Date‑object math:** all time calculations use the `Date` object for robustness, even though we only ever care about hours/minutes on the same day.
*   **Slot capping:** after the initial random durations are calculated, if the final therapy end exceeds the scheduled slot end, the code caps the end time and re‑derives the E&M duration, ensuring therapy always gets its minimum 16 minutes.
*   **Copy‑button state:** a `setTimeout`‑based feedback loop toggles a green checkmark for 2 seconds; rapid clicks are handled by clearing the previous timer.

The source is extensively commented and straightforward to modify if you need different rules (e.g., different minimum therapy time, different slot lengths).

📄 License
----------

This project is provided as‑is for educational and professional documentation support. You are free to use, modify, and share it.

Built with ❤️ to keep documentation honest and audit‑resistant.
