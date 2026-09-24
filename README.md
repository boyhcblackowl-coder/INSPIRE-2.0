# INSPIRE — GitHub PWA Wrapper

This package wraps the existing INSPIRE Apps Script Web App in an installable GitHub Pages PWA shell.

## Existing INSPIRE Web App
https://script.google.com/macros/s/AKfycbzsW1cYUPoJwd2R1xUDbSxFE6QM_qFsGyL4eYYGDwLtN5NtXa3EGe3vYz5wrPryAbIjCA/exec

## What this wrapper does
- Gives INSPIRE a clean GitHub Pages URL.
- Adds a proper web-app manifest.
- Uses Black Owl icons for Android/iPhone Home Screen.
- Runs in standalone display mode when installed.
- Adds a service worker for the wrapper shell.
- Shows a branded splash screen.
- Leaves the existing Apps Script login/backend unchanged.

Important: the Apps Script iframe is cross-origin, so its internal pages are NOT cached by the service worker.

## Files
- index.html
- manifest.webmanifest
- service-worker.js
- offline.html
- .nojekyll
- icons/icon-180.png
- icons/icon-192.png
- icons/icon-512.png
- icons/icon-maskable-512.png
- icons/favicon-64.png

## Deploy to GitHub Pages

### Option 1 — New repository
1. Create a new GitHub repository, e.g. `inspire-blackowl`.
2. Upload ALL files/folders in this package to the repository root.
3. Commit the files.
4. Open repository Settings.
5. Open Pages.
6. Under Build and deployment, choose `Deploy from a branch`.
7. Branch: `main`.
8. Folder: `/ (root)`.
9. Save.
10. Wait for GitHub Pages to publish.

Your URL will normally follow the GitHub Pages pattern for your account/repository.

### Option 2 — Existing repository
Put these files at the Pages publishing root. Keep relative paths unchanged.

## Test before installing
Test the GitHub Pages URL on:
- Android Chrome normal mode with multiple Google accounts logged in.
- iPhone Safari.
- Wi-Fi and mobile data.

Test specifically whether the embedded Apps Script loads without the previous `Sorry, unable to open` issue.

If the same multi-account issue still happens inside the iframe, the wrapper cannot remove Google's Apps Script account-session limitation. In that case the next architecture should use the GitHub frontend as the real UI and Apps Script only as a backend/API.

## Add to Home Screen

### Android
1. Open the GitHub Pages URL in Chrome.
2. Menu `⋮`.
3. Choose `Add to Home screen`, `Install app`, or `Create shortcut`.
4. Confirm `INSPIRE`.

### iPhone
1. Open the GitHub Pages URL in Safari.
2. Tap Share.
3. Tap `Add to Home Screen`.
4. Keep the name `INSPIRE`.
5. Add.

## Updating the Apps Script URL
If the INSPIRE `/exec` deployment URL ever changes, edit `index.html`.

Search for:
`https://script.google.com/macros/s/AKfycbzsW1cYUPoJwd2R1xUDbSxFE6QM_qFsGyL4eYYGDwLtN5NtXa3EGe3vYz5wrPryAbIjCA/exec`

Replace both occurrences with the new `/exec` URL.

Then change the cache version at the top of `service-worker.js`, for example:
`inspire-wrapper-v1.0.0` → `inspire-wrapper-v1.0.1`

Commit/push again.

## Custom domain later
This wrapper is compatible with a custom domain such as:
`inspire.blackowl.id`

Set that only after the GitHub Pages pilot works reliably.

## Security note
This wrapper does NOT bypass INSPIRE login. Employee ID + PIN and session validation remain handled by the INSPIRE application/backend.
