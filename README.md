# LeetCode Hint Coach 📱

An iPhone-first study app built around a curated LeetCode/NeetCode problem list. It presents one problem at a time and reveals progressive hints without immediately exposing a solution.

## Current app

- 22 problems from the uploaded problem list.
- One-problem-at-a-time study flow.
- Three progressive hints per problem.
- Solved / review / skip state stored locally on the iPhone.
- Progress dashboard and review queue.
- Direct links to each NeetCode problem.
- Installable on iPhone as a Home Screen web app (PWA).
- Offline app shell through a service worker.
- GitHub Pages deployment through GitHub Actions.

## Run on iPhone

After GitHub Pages is enabled for this repository, open the deployed site in Safari on the iPhone and choose **Share → Add to Home Screen**.

## Architecture

The client is deliberately static: HTML/CSS/JavaScript plus a JSON question catalog. This keeps the core study experience simple and lets progress stay on-device.

### Google Docs continuous sync

The long-term sync design is intentionally separated from the client. A small authenticated sync service should use the Google Docs API to:

1. Watch the configured Google Doc for changes.
2. Fetch the document when it changes.
3. Extract new/changed LeetCode URLs.
4. Diff them against the catalog.
5. Add newly discovered questions while preserving local progress by stable URL.
6. Generate/store progressive hints server-side.

Do not put Google OAuth credentials or API secrets in the iPhone/PWA client.
