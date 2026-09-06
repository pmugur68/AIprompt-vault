# Prompt Vault v3.1 — Persistent Google Drive Sync + Mobile Menu

Prompt Vault is a local-first prompt library that works on phone and laptop and optionally synchronizes its data through your private Google Drive **App Data** area.

## What changed in v3.1

- Google Drive connection now survives a normal page refresh by preserving the active OAuth session for the browser tab/session.
- When a saved Google configuration exists but the session is no longer active, Prompt Vault attempts a quiet reconnect. If Google requires interaction, the app simply asks you to tap **Connect** again.
- Mobile no longer requires **Desktop site**. The bottom navigation now includes **Categories** and **More**.
- The **More** panel exposes Google Drive connection/status, Sync now, Drive settings, Export backup, and Import backup.
- Exact duplicate prompts are automatically collapsed during load/sync (same title, category, prompt text, and tags), helping clean up the duplicate sample prompt created during the initial multi-device setup.
- The service worker is now network-first when online, so GitHub Pages updates are picked up instead of being indefinitely hidden by an old cached copy.

## Google Drive setup

Use the existing Google Cloud OAuth Web Client you already created. The required scope remains:

`https://www.googleapis.com/auth/drive.appdata`

Your GitHub Pages origin should remain authorized, for example:

`https://pmugur68.github.io`

No Client Secret is used or required by Prompt Vault.

## Updating GitHub Pages

Upload/replace these files at the root of your GitHub repository:

- `index.html`
- `manifest.webmanifest`
- `sw.js`
- `README.md`

Commit the changes to `main`. GitHub Pages should redeploy automatically.

Because this release changes the service worker, the first visit after deployment may need one extra refresh. After the new service worker activates, later updates should appear normally.

## Mobile usage

Use the normal mobile site — **Desktop site should be OFF**.

The bottom navigation provides:

- All
- Favorites
- Add
- Categories
- More

**More** includes all Drive and backup controls.
