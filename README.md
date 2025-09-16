# Appointment Time Generator 🗓️

A simple, offline, browser-based tool for generating realistic E&M (Evaluation and Management) and therapy time slots for medical documentation.

This tool helps create varied and plausible time entries for 30-minute and 60-minute appointments, adding slight, randomized offsets to start times and durations to mimic real-world scenarios.

***

## ✨ Features

* **Two Appointment Types:** Supports both **30-minute follow-ups** and **60-minute initial evaluations**.
* **Smart Randomization:** Intelligently calculates E&M and therapy durations within logical constraints for each appointment type.
* **Time Variability:** Adds a small, random 0-2 minute delay to the start time for more realistic logging.
* **Strict Time Slots:** Ensures the generated total time never exceeds the scheduled 30 or 60-minute block.
* **Simple Interface:** Clean, easy-to-use interface that provides a clear, copy-paste-friendly output.
* **Fully Offline:** It's a single HTML file that runs entirely in your browser. No internet connection is needed after downloading.

***

## 🚀 Getting Started

You don't need to install any software to use this tool. Just download the file and open it.

1.  **Download the File**
    * Go to the `time.html` file in the code repository.
    * Right-click the **"Raw"** button and select **"Save Link As..."** or a similar option.
    * Save the file to a convenient location on your computer, like your Desktop or Downloads folder. Make sure the file name is `time.html`.

2.  **Open in Your Browser**
    * Navigate to where you saved the `time.html` file.
    * **Double-click the file.** It will automatically open in your default web browser (like Chrome, Firefox, Edge, or Safari).

That's it! The tool is ready to use.

***

## 💻 How to Use

Once the page is open in your browser:

1.  **Select Appointment Type:** Choose either **30-Min Follow-Up** or **60-Min Initial Eval**.
2.  **Enter Start Time:** In the input box, type the scheduled start time of the appointment in a 4-digit **HHMM** format.
    * Example: For 9:00 AM, enter `0900`.
    * Example: For 2:30 PM, enter `1430`.
3.  **Generate:** Click the **Generate** button.
4.  **Copy Output:** The generated times will appear in the box at the bottom. You can highlight and copy this text to paste into your documentation.

### Example Output

If you select a 30-minute appointment and enter a start time of `1500`, the output might look something like this:

E&M: 1501 to 1512 (11 minutes)

18 minutes therapy

Therapy start time 1512, stop time is 1530

(Total time: 29 minutes)
