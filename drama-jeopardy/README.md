# From Script to Stage: solo drama Jeopardy

Built September 18, 2026, for Eric Martinsen’s Mapping California course. Local working draft requested by the instructor. Not published, assigned, or connected to Canvas grades.

## Try it

Open [index.html](index.html) in a current browser. The entire game is in that one file, including its styles, clue data, explanations, glossary, and JavaScript. It requires no installation, account, API key, paid service, media download, or build step. It also works locally without an internet connection once the file is available.

Students choose a square or use **Pick a clue for me**, select an answer, and receive an explanation. **Next unplayed clue** moves through the remaining board. **Show me and explain** is always available. Completed clues remain openable for review; reopening them does not earn points again.

- Five categories, 25 clues, and 15 glossary terms from the instructor’s proposed glossary.
- Application-based situations, with explicit distinctions between observations and interpretations.
- Private first-choice practice points, with no timer, penalties, opponents, or rankings. Students can hide their point total in **How to play**.
- A final invented scene using Notice → Name → Interpret, a possible reading, and an alternative. This is a practice invitation, not an additional submission requirement.
- Responsive layout, native buttons and dialogs, visible keyboard focus, and Escape/focus-return behavior.
- Progress stored only in the browser when storage is available. No analytics, external assets, answer transmission, gradebook integration, or LTI connection is built into the file.

All scenes are invented. None quotes the play or claims to describe an actual production. The small Los Angeles examples invite contextual analysis without making California a required explanation for every scene. No new AI-use, grading, deadline, or completion policy is established here.

## Put it in Canvas

**The game needs an HTTPS hosting address before it can function as a student-facing Canvas embed.** A local file path or localhost preview address will not work for students.

1. Place **index.html** on an institution-approved static web host that serves it as HTML and permits iframe embedding. Use an existing hosting arrangement if available. A hosting provider’s ordinary access logs are separate from this game’s behavior.
2. Open the resulting HTTPS URL directly and check that the board responds to a clue selection. A repository source-code page, file download link, or sharing preview is not the game URL.
3. In [canvas-embed.html](canvas-embed.html), replace **both** copies of `https://YOUR-HOST.example/drama-jeopardy/index.html` with that actual URL.
4. Create or edit the intended Canvas Page. A suitable page title is **From Script to Stage: Drama Jeopardy**. Paste the fragment into its HTML editor. Do not paste the full game source into the Rich Content Editor.
5. Save and inspect the page in Student View before publication. Try a clue and the glossary in the embedded frame, then the new-tab link. Check both desktop and a narrow/mobile view. The iframe has its own vertical scroll; the new-tab route gives students more room.

Canvas’s [official HTML Editor Allowlist](https://community.instructure.com/en/kb/articles/387066-canvas-html-editor-allowlist) permits iframe elements and associated attributes, while script elements are absent from the allowed page content. That is why the template embeds the game as a separate document. This does not verify the institution’s domain restrictions or a chosen host’s iframe headers. The iframe uses `allow-scripts allow-same-origin` to support the game and its browser-local progress storage; it should point to the separate approved host, not arbitrary untrusted content.

Uploading an HTML file to Canvas Files is not the verified deployment route for this build. File preview and script handling can differ. A successful local test does not establish a successful Canvas import, embed, mobile-app experience, or publication.

## Progress and shared devices

Only clue selections and the points-visibility preference are stored, under `c1003-drama-jeopardy-v1`. There are no student names or typed responses. On a shared browser profile, another person could see the prior board; **Start over** clears that game’s progress after a confirmation. Clearing browser data also removes it. Private browsing and embedded third-party storage restrictions may prevent saving, in which case the game continues in memory and displays a notice. Embedded and standalone storage may be partitioned separately by the browser.

This is a practice tool. It does not prove participation, certify mastery, or report completion to an instructor. The displayed score can be changed by a technically knowledgeable user, as with any client-only game.

## Edit the questions

Find `<script id="game-data" type="application/json">` near the middle of **index.html**. Each clue has an ID, category index, value, scene, question, four options, zero-based answer index, explanation, and a connection to close reading. The three glossary clusters are in the same data block.

Preserve valid JSON. If you materially change answers or clue identities, increment the data `version` so previously saved responses do not get treated as answers to the revised board. The interface derives points from the clue values. The current five-by-five board totals 7,500 possible points. This file is intentionally a small standalone component, not a general quiz authoring system.

## Files and scope

- [index.html](index.html): complete game.
- [canvas-embed.html](canvas-embed.html): Canvas HTML fragment with an explicit hosting placeholder.
- [QA.md](QA.md): actual local verification and remaining checks.
- `decisions/instructor_design_decisions.md`, entry C1003-D055: the bounded build request and authority status.

No course cartridge, module, assignment, homepage, source archive, or live Canvas item was changed for this component. No public hosting or commit was performed. The next deployment step is choosing the real hosting URL, then checking the embed in the course.
