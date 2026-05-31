# 🔥 Vibrant Resonance — Burma Shave Sign Voting
### Critical Northwest 2026

A community voting tool for Burma Shave signs at [Critical Northwest](https://criticalnw.org), a regional Burning Man event in the Pacific Northwest. The playa community votes on which one-liner signs to display as participants enter the event — and can submit their own.

---

## What it does

- Displays a list of candidate Burma Shave signs
- Anyone can upvote or downvote signs
- Anyone can submit a new sign
- Votes and submissions are shared in real time across all devices
- Signs are ranked by vote count
- Submitted signs are screened by an AI content filter before going live

---

## Deploying it

The entire app is a single HTML file — no framework, no build step, no server.

**To deploy on Netlify (recommended):**
1. Fork or clone this repo
2. Go to [app.netlify.com](https://app.netlify.com) and create a new site from Git
3. Point it at this repo, set the publish directory to `/`
4. Deploy — done

Or use **Netlify Drop**: drag `cnw-burma-shave.html` onto [app.netlify.com/drop](https://app.netlify.com/drop) for an instant one-off deploy.

**Data storage:**
Votes and signs are stored in a [JSONBin](https://jsonbin.io) bin. To run your own instance:
1. Create a free account at jsonbin.io
2. Create a new bin with content `{"signs": []}`
3. Generate an API key
4. In `cnw-burma-shave.html`, replace the `BIN_ID` and `API_KEY` values near the top of the `<script>` section:

```js
const BIN_ID  = 'your-bin-id-here';
const API_KEY = 'your-api-key-here';
```

---

## Updating the signs list

The seed signs are defined in the `SEED` array in the `<script>` section of the HTML file. These are loaded into JSONBin the first time the page runs on an empty bin.

To change the default signs:
1. Open `cnw-burma-shave.html` in any text editor
2. Find the `const SEED = [...]` array
3. Add, remove, or edit the strings — one sign per line, comma-separated
4. **Important:** if the JSONBin already has data, changing SEED won't affect it — the seed only loads when the bin is empty. To reset to your new list, go to jsonbin.io, open your bin, and replace its contents with `{"signs": []}`, then reload the page.

---

## Content filter

Every sign submission passes through a two-stage filter before being saved:

**Stage 1 — Regex pre-check**
A list of regular expressions catches common slurs and hate speech patterns instantly, including common letter-substitution tricks (e.g. `1` for `i`, `3` for `e`).

**Stage 2 — AI moderation**
If the regex passes, the text is sent to Claude (Anthropic's AI) with a moderation prompt. The prompt is tuned for a burn event context — crude, weird, and edgy humor is explicitly allowed, but targeted hate speech, slurs, and harassment are blocked. This makes the filter much harder to circumvent than a word list alone.

If the AI call fails due to a network issue, the app fails open (the regex still runs, but the AI check is skipped) so that connectivity problems don't prevent legitimate submissions.

Blocked submissions show the message: *"That sign was blocked — keep it weird, not hateful."*

---

## Admin mode

There is a password-protected admin mode that adds a Delete button to every sign card. Access it via the subtle `···` button in the page footer. The password is managed by the event organizers and is not stored in this repository.

---

## Built with

- Vanilla HTML/CSS/JavaScript — no dependencies
- [JSONBin](https://jsonbin.io) for shared real-time data storage
- [Anthropic Claude API](https://anthropic.com) for AI content moderation
- [Google Fonts](https://fonts.google.com) — Oswald + Inter
- Deployed on [Netlify](https://netlify.com)

---

*Made with ❤️ and a little bit of forest magic for Critical Northwest 2026 — Vibrant Resonance.*
