🗓️ Appointment Time Generator
==============================

**A completely offline, single‑file HTML tool** that creates realistic, audit‑defensible time entries for E&M (Evaluation & Management) and add‑on psychotherapy services. Now with flexible session lengths, three add‑on code options (90833, 90836, 90838), and dynamic feasibility checks.

Designed for psychiatrists and mental health providers who need to document time‑based split billing (E&M + therapy) in a way that mirrors real‑world practice while satisfying strict payer documentation requirements.

**Why this exists:** Insurance companies are increasingly using AI‑powered audits to scrutinize notes with add‑on psychotherapy (CPT codes +90833, +90836, +90838). They now often require exact start/stop times and expect discrete, stopwatch‑measured blocks — something no real clinical encounter follows. This tool helps you generate plausible, varied time logs that stay on the right side of an AI audit without fabricating information.

✨ Features
----------

*   **Flexible session length:** Enter any number of minutes (e.g., 30, 45, 60, 92, 120). The tool no longer limits you to fixed 30‑ or 60‑minute slots.
*   **Three add‑on therapy codes:**
    *   `90833` – requires 16‑37 minutes of therapy
    *   `90836` – requires 38‑52 minutes of therapy
    *   `90838` – requires 53+ minutes of therapy
*   **Feasibility guard:** If the chosen session length cannot accommodate the selected code’s minimum therapy time (after the random start offset), the tool displays _“This combination is impossible.”_
*   **Clinically plausible randomization:**
    *   Total encounter time is randomly chosen within a small window just before the scheduled end (up to 4 minutes short), never unrealistically far from the slot boundary.
    *   E&M duration is always at least 9 minutes.
    *   The therapy portion is randomly drawn within the allowed range of the selected code while preserving the 9‑minute E&M floor.
*   **Natural start‑time variation:** Every generated appointment begins 0‑3 minutes after the entered clock time, mimicking typical practice (knock on the door, walking to the room, etc.).
*   **Strict slot enforcement:** If the random start offset plus the required minimum times would exceed the session length, the tool immediately warns you. Otherwise, it guarantees the encounter ends within 4 minutes of the scheduled block end.
*   **Copy‑to‑clipboard:** One‑click copy with visual confirmation (green checkmark).
*   **Self‑contained offline app:** No dependencies, no network requests — download it once and it works forever.
*   **Opinionated UX:** After each generation, both the session length and the add‑on code revert to their defaults (30 minutes, 90833) to prevent accidental carry‑over of unusual settings.

📋 How the Randomization Works
------------------------------

The tool’s internal logic ensures that every generated time split is both **clinically reasonable** and **audit‑defensible**.

1.  **User provides:** scheduled start time (HHMM), session length (minutes), and add‑on code.
2.  A random start offset (0‑3 min) is applied to the scheduled start minute.
3.  The _available time_ = session length – offset (maximum possible encounter length).
4.  The tool verifies: (minimum therapy for that code + 9‑minute E&M) ≤ available time. If not, it reports “impossible”.
5.  A **total encounter duration** is randomly chosen between the minimum needed (E&M min + therapy min) and the available time, but never less than (available time – 4 minutes). This keeps the end close to the slot boundary.
6.  The therapy duration is then randomly selected within the code’s allowed range, but capped so that at least 9 minutes remain for E&M.
7.  E&M duration = total – therapy (guaranteed ≥ 9).
8.  The times are calculated and displayed, showing start, E&M end, therapy end, and minute totals.

🚀 Getting Started
------------------

### 1\. Download

Grab the file `time.html` (the only file in the repository). Click the “Raw” button and **Save As…** or simply copy the source. Save it to a convenient location on your computer (Desktop, Documents, etc.).

### 2\. Open

Double‑click the file — it will open in your default web browser. No internet connection is required.

### 3\. Use

*   Enter the **session length** in minutes (default: 30).
*   Select the appropriate **add‑on code**:
    *   `90833` – 16‑37 min therapy
    *   `90836` – 38‑52 min therapy
    *   `90838` – 53+ min therapy
*   Enter the scheduled start time in **HHMM** format (24‑hour clock).
    *   Example: 9:00 AM → `0900`
    *   Example: 2:30 PM → `1430`
*   Click **Generate**.
*   The output box shows the exact times and durations. Click the 📋 button to copy everything to your clipboard.

📊 Example Outputs
------------------

**30‑minute session, 90833, start 1200:**

    Add‑on code 90833
    E&M start 1202, end 1214 (12 minutes)
    Add‑on psychotherapy start 1214, end 1229 (15 minutes)
    Total encounter time: 27 minutes

**55‑minute session, 90833, start 1200:**

    Add‑on code 90833
    E&M start 1201, end 1215 (14 minutes)
    Add‑on psychotherapy start 1215, end 1252 (37 minutes)
    Total encounter time: 51 minutes

**60‑minute session, 90836, start 0900:**

    Add‑on code 90836
    E&M start 0903, end 0914 (11 minutes)
    Add‑on psychotherapy start 0914, end 0957 (43 minutes)
    Total encounter time: 54 minutes

⚠️ Important Notes
------------------

**This tool is not a substitute for clinical judgment.** Always ensure that the generated times reflect the actual work performed. The purpose is to provide plausible, varied documentation templates that match real‑world variability — not to create false records.

*   The tool always resets to **30 minutes** and **90833** after each generation (by design).
*   All time calculations happen in your browser; no data is sent anywhere.
*   The regex‑based input validation rejects times like `2500` (invalid hour) — only `00`‑`23` are accepted.
*   If the selected code demands more therapy minutes than the session length (minus start offset and E&M minimum) allows, the tool displays an “impossible” message rather than producing an invalid split.

🧠 Under the Hood (for developers)
----------------------------------

The tool is a single HTML file with embedded CSS and vanilla JavaScript. Key design decisions:

*   **No external libraries:** everything is plain JS, including the clipboard interaction (using the `navigator.clipboard` API).
*   **Date‑object math:** all time calculations use the `Date` object for robustness, though we only care about hours/minutes on the same day.
*   **Soft shortfall limit:** a `SHORTFALL_MAX` constant (currently 4 minutes) keeps the total encounter close to the scheduled block end, preventing unrealistic early finishes.
*   **Feasibility check:** before randomizing durations, the tool confirms that the minimum therapy + minimum E&M ≤ available time. If not, it immediately aborts with a clear message.
*   **Copy‑button state:** a `setTimeout`‑based feedback loop toggles a green checkmark for 2 seconds; rapid clicks are handled by clearing the previous timer.

The source is extensively commented and straightforward to modify if you need different rules (e.g., different minimum therapy time, different shortfall allowance).

📄 License
----------

This project is provided as‑is for educational and professional documentation support. You are free to use, modify, and share it.

Built with ❤️ to keep documentation honest and audit‑resistant.
