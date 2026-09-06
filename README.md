# Prompt Vault v2 — Google Drive Sync

Prompt Vault is a local-first prompt library for phone and laptop. It works offline and can optionally synchronize its data through your own Google Drive account.

## What’s new in v2

- Google Drive App Data sync
- Local-first/offline operation
- Automatic or manual synchronization
- Merge protection for edits made on multiple devices
- Deletion tombstones to prevent deleted prompts from reappearing after sync
- Visible sync status and Sync Now control
- Existing categories, tags, favorites, search, prompt variables, one-click copy, backup/import

## Important: Google sign-in requires the app to be hosted

Google OAuth does not work reliably from a `file://` address. To use Drive sync, host the `prompt-vault` folder on an HTTPS address. GitHub Pages, Netlify, Cloudflare Pages, Firebase Hosting, or any normal HTTPS web host will work.

## One-time Google Cloud setup

1. Open Google Cloud Console and create/select a project.
2. Enable **Google Drive API**.
3. Configure the OAuth consent screen. For a personal app, add your Google account as a test user if the app is still in Testing status.
4. Create **OAuth Client ID → Web application**.
5. Under **Authorized JavaScript origins**, add the exact HTTPS origin where Prompt Vault is hosted, e.g. `https://yourname.github.io`.
6. Copy the generated Client ID. It ends in `.apps.googleusercontent.com`.
7. Open Prompt Vault → **Google Drive settings** → paste the Client ID → **Save & Connect**.
8. Approve the requested Google Drive permission.

Prompt Vault requests only the `drive.appdata` scope. This lets it read/write files created inside its private application-data area. It does not request access to your normal Google Drive documents.

## Cross-device use

Use the same hosted Prompt Vault URL and the same Google account on your phone and laptop. Enter the same OAuth Client ID once on each device and connect. The local library remains available offline and syncs when online.

## Files

- `index.html` — app
- `manifest.webmanifest` — installable PWA metadata
- `sw.js` — offline service worker

## Backup

Even with Drive sync, Prompt Vault keeps the manual JSON Export/Import feature. Keeping occasional exports is recommended for important prompt libraries.
