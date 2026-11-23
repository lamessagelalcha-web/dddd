# Dembi Dolloo Online Exam System

A single-file, browser-based online exam portal for Grade 12 National Examination preparation, built for **Waajjira Barnoota Magaalaa Dambi Doolloo** (Dembi Dolloo Town Education Office).

Everything lives in one file, `kena.html`: HTML, CSS and JavaScript. There is no build step and no server code.

## Features

### Students
- Self-registration (full name, email, username, password, stream)
- Streams: Natural Science and Social Science
- Three built-in subjects: Mathematics, English, Aptitude
- 60 multiple-choice questions per subject
- 2-hour countdown timer per exam, with automatic submission when time runs out
- Question navigator showing the current question and answered questions
- Previous / Next navigation and a jump-to-question grid
- Instant results: score %, correct count, total questions, and a per-question review with correct answers
- Personal results history on the dashboard

### Admin
- Password-protected admin dashboard
- Stats: total registered students and active exams
- Table of all registered students (username, email, stream, exam status, score)
- Question management UI: subject selector (including a custom subject) and PDF/DOCX upload field
- Reset questions by subject

## Getting Started

1. Put `kena.html` anywhere you like.
2. Open it in a modern browser (Chrome, Edge, Firefox, Safari).
3. Choose **Student Login** or **Admin Login**. New students click **Register here**.

An internet connection is needed on first load for these CDN libraries:
- Tailwind CSS (`cdn.tailwindcss.com`)
- Lucide icons (`cdn.jsdelivr.net`)

## Usage

**Student flow:** Register, log in, pick a subject, answer the questions, then press **Submit Exam** (or wait for the timer). Results appear immediately.

**Admin flow:** Choose Admin Login, enter the admin password, then view students and manage questions.

## Project Structure

```
kena.html   # Entire app (markup, styles, scripts, question bank)
README.md   # This file
```

Key parts of `kena.html`:

| Part | Purpose |
|------|---------|
| `questionsDatabase` | Built-in question bank (`mathematics`, `english`, `aptitude`) |
| `loginStudent()`, `loginAdmin()`, `registerStudent()` | Authentication and registration |
| `startExam()`, `displayQuestion()`, `startTimer()`, `submitExam()` | Exam engine |
| `updateStudentsTable()`, `updateAdminStats()` | Admin views |

## Adding or Editing Questions

Questions are plain JavaScript objects in `questionsDatabase`:

```js
{ id: 1, text: "What is 7 × 8?", options: ["54", "56", "60", "50"], correct: 1 }
```

`correct` is the zero-based index of the right option in `options`.

## Data Storage

Student accounts and scores are stored in the browser's `localStorage` under the key `students_data`. This means:
- Data exists only in the browser and on the device where it was created.
- Clearing browser data erases all accounts and results.
- Students and the admin on different computers do not see each other's data.

## Known Limitations

This is a demo/prototype and is **not ready for real high-stakes exams** as it stands:

- **Admin password is hardcoded** in `loginAdmin()` in the page source, so anyone can read it. Change it before use.
- **Student passwords are stored in plain text** in `localStorage`.
- **No server-side storage or authentication**, so scores can be edited from the browser console.
- **Admin dashboard shows no students**: `showAdminDashboard()` calls `updateAdminStats([])` and never loads saved students into the table.
- **Question upload is a placeholder**: the PDF/DOCX upload only shows a success message and does not parse or save anything.
- **Reset Questions is a placeholder**: it shows a confirmation message but does not change the question bank.
- **Only the latest result is kept per student**, not one per subject.
- **No anti-cheating measures** (no tab-switch detection, no question shuffling).
- Some answer options and question wording in the bank may need review before real use.
- The page references `/_sdk/element_sdk.js` and `/_sdk/data_sdk.js`, which only exist on the original hosting platform. They are optional, and the app falls back to `localStorage` without them.

## Suggested Next Steps

- Move accounts, questions and results to a backend (e.g. Firebase, Supabase, or a Node/PHP API) with hashed passwords
- Implement real question import and reset
- Load students into the admin table and add result export (CSV/Excel)
- Randomize question and option order
- Store a result per subject attempt

## License

No license specified. Add one if you plan to share or distribute this project.
