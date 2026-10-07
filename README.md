# Alcove Free for Chrome

A calm new tab for your browser: tasks, habits, notes, a focus timer and meditation, in zones you arrange yourself.

Alcove Free replaces your new tab page. Everything is stored locally in your browser. There is no account, no server and no tracking.

Website: <https://alcovehq.ca> · Privacy: <https://alcovehq.ca/privacy> · Terms: <https://alcovehq.ca/terms>

**Version:** 0.9.3

## Features

### Zones
- Home screen of resizable, draggable zones on a 4-column grid: Tasks, Habit tracker, Pomodoro timer, Meditation, Notes.
- Open only the zones you want ("Manage zones"). Layout is saved automatically.
- Time-of-day greeting with your name and today's stats (tasks done, focus minutes, meditation minutes, habits).

### Tasks
- Full task list with nested **tags**, sidebar filters (All, Must do, Should do, Untagged) and Open / Done views.
- **Lanes:** pull tasks into the red (Must do) and yellow (Should do) lanes on the home screen, by click or drag and drop.
- **Deadlines** with a date picker and **repeating tasks** (daily, weekdays, weekly, monthly, yearly, or custom intervals with an end date or count).
- **Month calendar** under the list. Drag a task onto a day to reschedule it. Repeats appear as ghost chips.
- Per-task side sheet with markdown notes and checklists (`- [ ]`).
- Toolbar badge shows the number of open tasks in your lanes.

### Habit tracker
- Day-by-day grid. Click to check, double-click to skip (a skip keeps the streak; max two in a row).
- Current streak, best streak, 7/30/365-day counts and a 30-day consistency score.
- Scroll back through history and zoom the grid.

### Pomodoro and stopwatch
- Focus, short break, long break loop (focus, short, focus, long). Lengths are configurable.
- Stopwatch mode for open-ended sessions.
- Timers keep running with the tab closed. A background script fires a notification when one finishes.
- Today's focus sessions and minutes are tracked (last 90 days kept).

### Meditation
- 3, 5, 10 or 15 minute sessions with a breathing orb (5.5 s in, 5.5 s out).

### Notes
- Up to 500 markdown notes with a live-preview editor (headings, bold, links, task lists, quotes, code), saved as you type.
- Press `Ctrl/Cmd+Enter` to save and close.

### Personalise and back up
- Light and dark themes, seven accent colours, your name for the greeting.
- Export everything to a JSON file and import it on another computer (Settings, Back up & restore).

## Install

This repository contains the **built** extension (no `src/` directory), so there is no build step to run.

### Firefox (version 142 or later)
Uses `manifest.json`.

1. Open `about:debugging#/runtime/this-firefox`.
2. Click **Load Temporary Add-on…** and choose `manifest.json`.

Temporary add-ons are removed when Firefox restarts. For a permanent install, package and sign it through [addons.mozilla.org](https://addons.mozilla.org).

### Chrome / Chromium (Manifest V3)
Chrome needs a service worker instead of the Firefox-style background script, so use `manifest.chrome.json`.

1. Copy the repo to a new folder (or a `chrome/` build directory).
2. In that copy, delete `manifest.json` and rename `manifest.chrome.json` to `manifest.json`.
3. Open `chrome://extensions`, enable **Developer mode**.
4. Click **Load unpacked** and select the folder alcove_chrome_0.9.3

## Permissions

| Permission | Why |
| --- | --- |
| `storage` | Save your tasks, habits, notes and settings locally. |
| `alarms` | Wake the background script when a timer ends, and for hourly housekeeping. |
| `notifications` | Tell you when a Pomodoro or meditation finishes (can be switched off in Settings). |

Alcove makes no network requests. The only outbound links are the website, privacy and terms links in the UI.

## Project layout

```
manifest.json          Firefox manifest (MV3, background.scripts)
manifest.chrome.json   Chrome manifest (MV3, background.service_worker)
index.html             New tab page
background.js         Timer completion, notifications, badge count, toolbar icon colour
assets/
  index-*.js           App bundle (React 18)
  LiveEditor-*.js      Lazy-loaded CodeMirror markdown editor
  index-*.css          Styles (fonts are bundled locally)
icons/                 Extension icons and alcove-mark.svg
```

## Data and storage

All data lives in `storage.local` under these keys: `tasks`, `tags`, `habits`, `notes`, `settings`, `pomodoro`, `meditation`, `stopwatch`, `stats`, `layouts`, `openZones`. Everything read from storage (including imported backups) is validated and clamped before use.

Limits: 500 notes, 50,000 characters per note, 20,000 characters per task note.

To wipe everything, use **Settings, Erase all data**, or remove the extension.

## Tech

React 18, TypeScript and Vite (bundled output), CodeMirror 6 for editing. Written against the WebExtensions API and works with either the `browser` or `chrome` namespace.

## Licence

Copyright the Alcove authors. All rights reserved unless a licence file says otherwise.
