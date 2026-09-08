# Prompt Vault v3.5.3 — Persistent Google Drive Sync + Mobile Menu

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


## v3.5.3
- Added **Export to Excel** on desktop and mobile.
- Exports prompts as `prompt-vault-prompts.xlsx` with Title, Category, Tags, Prompt, and Favorite columns.


## v3.5.3
- Rename categories with ✎.
- Set a parent category to create subcategories.
- Drag prompt cards onto categories on desktop/laptop to move them.
- On phones: Edit prompt → Category → Save to move it reliably.

## v3.5.3 fixes
- Fixed the Manage Category window so it opens as a proper centered modal instead of appearing permanently at the bottom of the page.
- Fixed desktop drag-and-drop initialization after prompt cards render.
- New Category now includes an optional Parent Category selector, so subcategories can be created directly.
- Parent choices are limited to main categories to keep the hierarchy to one subcategory level.
- Added a visible v3.5.3 marker in the sidebar footer for deployment verification.

## v3.5.3 sidebar fix
- Fixed categories disappearing on laptops with shorter browser windows.
- The category list now has its own guaranteed visible/scrollable area.
- The whole sidebar can also scroll when the screen height is limited.

## v3.5.3 category-tree fix
- Fixed subcategories being displayed under the wrong parent. The sidebar now renders a real parent/child tree instead of sorting all categories only by depth.
- Parent categories with children now show ▾ / ▸ expand-collapse controls instead of #.
- Subcategories remain indented beneath their actual parent.
- Collapse state is remembered and included in the synced database.

## v3.5.3
- Rebuilt sidebar rendering as a true parent-child tree.
- Subcategories now render only below the parent stored in categoryParents.
- Parent categories show ▾ / ▸ instead of #.
- Added a cache reset and versioned service-worker registration to stop laptops from remaining on older deployed HTML.
- Online navigation now uses fresh network content first; cache is only an offline fallback.

## v3.5.3 category controls
- Case-only renaming now works (for example `Job Search` → `JOB SEARCH`).
- Parent chevrons are dedicated clickable expand/collapse controls.
- Categories themselves can now be dragged onto another main category to become subcategories.
- Drag a subcategory to “Drop here to make main category” to move it back to the top level.
- Prompt-card drag/drop remains supported separately.

## v3.5.3 file attachments
- Attach multiple files directly to a prompt.
- Supported picker types include images, PDF, Word, Excel, PowerPoint, TXT, and CSV.
- Attachments are saved inside the prompt record and therefore included in Prompt Vault JSON backup and Google Drive App Data sync.
- Individual files are limited to 5 MB.
- Attached files can be previewed/opened from the prompt editor and removed before saving.
- Prompt cards show attachment names.
- Excel export lists attachment file names.

## v3.5.3 category deletion
- Added **Delete category** to the Manage Category window.
- Deletion requires a second confirmation: “Are you sure you want to delete this category?”
- Prompts from a deleted category are moved to **Uncategorized** so prompt content is not lost.
- Subcategories under a deleted parent become main categories.

## v3.5.3 category deletion sync fix
- Deleted categories no longer reappear after Google Drive sync.
- Category deletions now create synced tombstones.
- Category create/rename/reparent actions carry timestamps so newer changes win over older cloud state.
- Renaming also tombstones the old category name, preventing the old spelling/name from returning.
- Merge logic removes deleted categories and cleans stale parent/collapse references.

## v3.5.3 Home + Search redesign
- Replaced **All Prompts** with **Home** on desktop and mobile.
- Home lists categories alphabetically, with subcategories directly beneath their parent.
- Desktop Home shows category cards with prompt counts and subcategory rows.
- Replaced the mobile **Categories** button with a classic magnifying-glass **Search** button.
- Added a dedicated Search page with a keyword field and a Prompt / Category selector.
- Prompt search returns prompt cards with Edit, Copy, Favorite, tags, category, and attachments.
- Category search returns matching categories with parent path and prompt count.
- Added Search to desktop navigation.
- Ctrl/Cmd + K opens Search.
- Existing category management, drag/drop, attachments, Excel export, backups, and Google Drive sync remain.

## v3.5.3 Google Drive settings fix
- Fixed a JavaScript runtime error introduced by the v3.5 mobile navigation redesign.
- The removed `mobileNewCategory` control still had an old click-handler assignment; this stopped later initialization code from running.
- Google Drive Settings, Connect, Sync Now, Save & Connect, and Disconnect handlers now initialize normally on desktop and mobile.


## v3.5.3 mobile prompt-save fix
- Fixed prompt saves failing on phones when attachment data filled browser localStorage.
- Actual attachment file data is now stored in IndexedDB; prompt records keep only lightweight attachment metadata.
- Google Drive sync and JSON backup still carry the full attachment data.
- Existing inline attachment data is migrated automatically.
- Added a UUID fallback for mobile browsers/webviews.
- The editor now closes only after a successful local save, so failed saves are visible instead of silently losing the prompt.

## v3.5.3 app icon
- Added a custom Prompt Vault app icon.
- Added Android/PWA icons at 192×192 and 512×512.
- Added a 180×180 Apple touch icon for iPhone/iPad Home Screen.
- Added a 32×32 browser favicon.
- Updated the web app manifest for standalone installation.
- Preserves all v3.5.2 mobile-save and attachment-storage fixes.
