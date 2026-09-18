## Deployment notes

Pipeline: Claude drafts → GitHub stores → Netlify auto-deploys on push →
iframe embed in a Canvas page.

### Gotchas, in the order they bit

**Netlify team protection is on by default.** A protected site redirects
every request to `app.netlify.com/edge-access` for a login, so the Canvas
iframe shows a grey box and the console reports a `frame-ancestors` CSP
violation plus a 401. The error names `app.netlify.com`, not your site,
which sends you hunting in the wrong place. Fix: Project configuration →
Access & security → turn team protection off.

**Test in a browser where you are logged out of Netlify.** Signed in, a
protected site looks fine and you learn nothing. Students have no Netlify
account, so the logged-out view is the only true test. Keep a second
browser for this, or use a private window.

**Canvas keeps `sandbox` and `loading` on the iframe.** Verified — it does
not strip them. `sandbox="allow-scripts allow-same-origin"` is what lets
the game write to `localStorage`. Drop `allow-same-origin` and progress
saving fails silently.

### Setup checklist for the next game

- [ ] `index.html` at the publish root; build command empty, publish
      directory `.`
- [ ] Rename the Netlify site before pasting any URL into Canvas —
      renaming changes the URL
- [ ] Load the bare Netlify URL and play one clue before touching Canvas
- [ ] Paste the fragment via the Canvas `</>` HTML editor, not the rich
      text view
- [ ] Check the saved page logged out, then in Canvas Student View
- [ ] Play a clue, reload, confirm the progress counter persisted
- [ ] Look at it on a phone — the iframe is a fixed 1050px tall

### Known limits

`localStorage` is per browser and per device. A student who starts in a
lab and finishes on a phone loses the counter. Fine for practice; do not
use the in-game count as evidence of completion.

### Repo structure for multiple games

One repo, one Netlify site, a folder per game:
# Local verification: From Script to Stage

Verified September 18, 2026. These are local checks, not evidence of Canvas import or live student access.

## Content and structure

- Confirmed 25 unique clue IDs, five categories with values 100 through 500, four options per clue, valid answer indexes, and explanations plus interpretive connections for every clue.
- Confirmed all 15 instructor-proposed glossary terms appear in the three clusters.
- Reviewed the copy for observation/inference distinctions, overlap between terms, objective versus tactic, and the difference between what a script specifies, suggests, or leaves open.
- All mini-scenes and the final challenge are identified as invented. No play text, footage, transcripts, or actual student materials are included.
- No em dashes in the game. Static element IDs are unique. No external scripts, fonts, images, or network calls are required by the game.

## Logic checks with Node

- JavaScript parses successfully after revisions.
- Fresh state starts at zero; all correct answers total 7,500 points.
- Repeated answers and reopened clues cannot award points twice.
- Revealing an answer counts the clue as explored without awarding points; answering it later cannot retroactively earn points.
- Restoring valid results preserves the score. Unknown IDs, invalid answer indexes, and incompatible saved-data versions are discarded.
- A malformed stored JSON value is caught and starts a fresh board; blocked storage is handled separately.
- Core text contrast calculations: main text on paper 11.26:1; gold clue values on teal 4.88:1; light hero text on dark green 11.89:1; muted text on white 6.62:1. These checks are not a full accessibility audit.

## Browser checks

Tested through the Codex in-app browser against a loopback-only local HTTP server.

- Visually inspected the desktop board and a 390-pixel phone-width board.
- Displayed every clue in a complete run. Tested a correct answer, a different answer, answer reveal, next-unplayed navigation, completion at 25 of 25, and transition into the final scene.
- Opened and read the final example and alternative interpretation.
- Verified the correct first-choice score, unchanged score on review, and neutral treatment of a different answer.
- Reloaded and confirmed progress restoration. Hid points, reloaded, and confirmed the preference persisted. Correct-answer feedback respects the hidden-score preference.
- Opened the glossary from within a clue; Escape closed the glossary and returned focus to its trigger. Escape from the clue returned focus to the current board square. Enter opened a clue. A focus-return defect found during testing was corrected and retested.
- Tested both reset cancellation and confirmed reset. Cancellation preserved 25 explored clues; reset returned the board to zero while retaining the display preference.
- Tested random clue selection; closing without answering left progress unchanged.
- Checked document widths at 390, 320, and 768 pixels without horizontal page overflow. At 320 pixels, the long final-category clue’s dialog content fit its width and scrolled vertically. At 390 pixels, clue targets measured about 67 pixels wide.
- No JavaScript errors or warnings were recorded in the tested standalone page.

## Iframe check and limitations

A temporary wrapper outside the repository used the delivered embed fragment with its placeholder replaced by the local game URL. The game rendered inside the iframe and generated all 25 buttons, showing that its script initialized there. A second fixture omitted `allow-same-origin` to deny local storage: the board still rendered and displayed the intended storage-unavailable notice, without a console error.

The browser automation could inspect and render the child frame but returned a target-unavailable error when trying to activate its controls through locators, accessibility indices, and a screenshot-based click. Therefore **embedded interaction has not been certified**. The full interaction checks above were performed in the standalone page. The local file URL itself was not opened by browser automation because that URL was blocked by its browser policy; the local HTTP version was used for testing.

Still needed before students use it:

- Select an approved HTTPS host and replace both placeholder URLs in the embed fragment.
- Test the saved Canvas page in Student View, including clue selection, glossary access, keyboard navigation, new-tab fallback, and narrow-screen scrolling.
- Check institution-specific embedding restrictions, host frame headers, and the Canvas mobile app if students will use it.
- Conduct assistive-technology testing if a formal accessibility conformance claim is needed. No screen-reader or complete WCAG audit was performed.
- Confirm any required use, workload, module placement, or submission directions separately. The game itself creates none of those requirements.

## Scope

Created `index.html`, `canvas-embed.html`, `README.md`, and this file under `development/active/drama_jeopardy/`. Appended C1003-D055 to `decisions/instructor_design_decisions.md`, preserving earlier entries and unrelated working changes. No source export, cartridge, course map, gradebook, live Canvas item, or public host was changed. No commit was made. `git diff --check` passed at the scoped build check.
