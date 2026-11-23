# Ethically Me: revision test report

## Round 3: real writing in (23 Nov 2026)

- **Moments 1 to 6:** title, lens tags, Situation, Ethical Conflict, Ethical Lens, Theory link, My Decision and My Moral Insight are replaced with the author's text. Every old story is gone (search for "KodeKloud" or "quiz" finds nothing).
- **Moment 3:** fully replaced with "Calm Before Blame".
- **Contents, page titles, progress text and search:** all use the new titles.
- **Topic lines:** all six moments now show a TOPIC line. Moments 3 to 6 received the same topic line element Moments 1 and 2 use, added at the author's request. At 1440x900 the left pages still fit. At 1366x680 the left pages of Moments 3 to 6 scroll about 20px more than before.
- **Section 3:** all text from the author is in. The commitment reads "As a moral person, I commit myself to" + the closing statement. No placeholders remain.
- **Page 9 fit at 1440x900:** the content was about 115px taller than both page halves combined. To fit it, "My Values" now starts the right half (reading order unchanged). Page 9 also uses tighter spacing: line height 1.4, smaller opener icon, and less padding and margin. No wording or font size changed. Both halves fit at 1440x900.
- **Apostrophes:** straight apostrophes in the supplied text were set as typographic ones (’) to match the rest of the file.
- **Em dashes:** none in the file.

Overflow after the change (desktop numbers are extra scroll inside the page half, shown as left / right):

| Page | 1440x900 | 1366x680 |
|---|---|---|
| Moment 1 | fits / 40px | 55 / 183px |
| Moment 2 | fits / 112px | 55 / 226px |
| Moment 3 | fits / 112px | 32 / 247px |
| Moment 4 | fits / 112px | 11 / 226px |
| Moment 5 | fits / 64px | 32 / 205px |
| Moment 6 | fits / 112px | 32 / 247px |
| Page 9 | fits / fits | 113 / 167px |

At 768x1024 and 390x844 every page is a single scrolling column with no horizontal overflow.

Regression checks:
- **Cover transition:** opens and closes cleanly at all four sizes.
- **Page clicks:** an empty-area click turns the page; text clicks and drag-selection do not.
- **Keyboard:** arrows, Home and End work, and Next is disabled on page 9 of 9.
- **Search:** "categorical imperative" finds Moment 2 and highlights it, and "Rawls" finds Moment 6.
- **Reduced motion:** no animations run.
- **Phone:** simulated swipes turn forward and back, and vertical swipes are ignored.
- **Offline:** no console errors and no outside requests.

Not verified: Safari, Firefox, and swiping on a real phone.

## Round 2 edits (22 Nov 2026)

1. **Author name:** kept as "JOHN BENEDICT C. PANTALLA" in all 3 places. Not changed.
2. **Em dashes removed** (none remain in the file):

| Where | Before | After |
|---|---|---|
| Moment 1, Ethical Conflict (dashes 1 and 2) | ...without explicit permission—even due to an automatic system error—was fundamentally unfair. | ...without explicit permission, even due to an automatic system error, was fundamentally unfair. |
| Moment 2, Theory link (dash 3) | ...responding to the genuine needs of others—especially when they lack access to basic resources. | ...responding to the genuine needs of others, especially when they lack access to basic resources. |

3. **Contents at 1366x680:** a rule that applies only to desktop widths with a height of 720px or less. It tightens only the cover's Contents list: heading 1.5rem, gap .3rem, entry padding .38rem. All 9 entries now show with 59px to spare and no scrolling (screenshot: `contents-1366x680.png`). At 1440x900, 768x1024 and 390x844 the computed sizes are unchanged and the list still fits.
4. **Retest at all four sizes:**
   - **Cover transition:** opens and closes at every size, with 6 animations each way and no console errors. The opening and closing filmstrips were regenerated.
   - **Page-click navigation (1366x680):** clicking empty page space turns the page. Clicking text or after a drag-selection does not.
   - **Keyboard:** ArrowRight through to page 9 of 9 disables Next, and Home, End, ArrowLeft and Escape work.
   - **Search:** "even due to" finds the new Moment 1 wording and highlights it.
   - **Reduced motion:** opening, a page turn and closing run with 0 animations.
   - **Offline:** no requests besides the page itself.

Tested on 22 Nov 2026 in Chromium (Playwright), pages served from a local `127.0.0.1` server. Viewports: 1440x900, 1366x680, 768x1024, 390x844.

## What changed in index.html

1. **Cover transition rebuilt.** The closed cover is now the front board of the real open book. It is exactly the right half of the open spread (same height) and is panned by a quarter of the book width so it sits centred. Opening turns the cover on its left spine edge while the same book pans to centre. The real right page sits underneath the whole time. The inside face of the cover is a live copy of the real left page, so when the cover lands at 180 degrees, nothing changes. Closing plays the same keyframes in reverse. Phones (under 860px) show one page, so the cover is the whole page and it swings fully off to the left. Reduced motion switches state instantly with no animation.
2. **"DECISION OR REFLECTION" renamed to "MY DECISION"** on all six moments.
3. **Assigned theory tag** ("ASSIGNED THEORY" + theory name) added to the number row of each moment opener. This row adds no height, so pages that fit before still fit.
4. **New Section 3 spread, "The Moral Person I Am Becoming"** (`#growth`, page 9 of 9). It has headings for My Ethical Thinking, My Values, My Ethical Growth, and My Commitment with the stem "As a moral person, I commit myself to...". Each field holds a dashed box marked PLACEHOLDER. It is wired into the Contents list, page count, progress bar (aria-valuemax 9), search, the hash, End key and Next, and Return to Cover.
5. **Bug fix (pre-existing):** the page-corner turn hint was positioned 4px outside each page half. On desktop that put a small horizontal scrollbar under the right page and a 4px vertical scroll on both halves. The offset is removed.

No journal wording was changed.

## Results

| Check | 1440x900 | 1366x680 | 768x1024 | 390x844 |
|---|---|---|---|---|
| Closed book centred, same height as open spread | pass (centre 720) | pass (centre 683) | pass | pass |
| Cover text and button fit on the closed cover | pass | pass | pass | pass |
| First animation frame identical to resting closed book (pixel diff) | 0 px | 0 px | antialiasing only | antialiasing only |
| Last opening frame identical to the open spread (pixel diff) | 0 px | 0 px | 12 px | antialiasing only |
| Closing ends identical to resting closed book | 0 px | 0 px | 0 px | antialiasing only |
| Page halves fit without scrolling | all 9 fit | scroll inside halves (same as original) | single column scrolls | single column scrolls |
| Horizontal overflow | none | none | none | none |
| Arrow keys, Home, End, progress "Page 9 of 9", Next disabled on last page | pass | pass | pass | pass |
| Console errors | none | none | none | none |
| Requests other than the page itself | none | none | none | none |

Interaction checks (1440x900 unless noted):

- Click on an empty right-page area turns forward. An empty left-page area turns back.
- Clicks on paragraph text, on the theory tag, or after a drag-selection do not turn the page.
- A right-page click on the last spread does not turn (boundary).
- The Contents link "The Moral Person I Am Becoming" opens `#growth`.
- Search "commit myself" finds only Section 3. Enter opens it with 1 highlight.
- Search "Utilitarianism" finds Moment 1 (tag) and Moment 6 (old theory link).
- Escape on an open page closes to the cover, clears the hash, and focuses Open Journal.
- Resizing while closed keeps the book centred. The cover width equals half the open book and the heights match.
- While closed, Tab skips the hidden journal (it is `inert`) and reaches Open Journal.
- Reduced motion: open, page turn and close run with 0 animations and still change state.
- 390x844 phone: loading `#growth` opens directly. A right swipe goes back and a left swipe goes forward. A vertical swipe does not turn the page.

Filmstrips are in this folder: `filmstrip-open-<width>.png` and `filmstrip-close-<width>.png`. Frames were taken at fixed points on the 1400 ms timeline by pausing the animations.

### Known limits

- At the start of closing, the keyboard focus ring on the page disappears and text switches to the smoother rendering used for moving layers. Both changes are a few pixels.
- (Fixed in round 2) At 1366x680 the Contents list used to scroll by about 49px.
- Real-device touch was not tested. Swipes were simulated with touch events.
- Only Chromium was tested. Safari and Firefox were not run.

## Task 2: assigned theory audit

All six moments currently link a theory other than the one assigned. Moments 1 and 2 are included even though they were recently updated.

| Moment | Assigned theory | Current Ethical Lens text | Current Theory link names | Match? |
|---|---|---|---|---|
| 1 Subscription Auto-Renewal | Utilitarianism | Honesty and Accountability | Virtue Ethics | No |
| 2 Assisting a Relative | Deontology (Kantian Ethics) | Beneficence and Care Ethics vs Responsibility to Self | Care Ethics | No |
| 3 Declining to Share Answers (to be replaced) | Aristotle's Virtue Ethics | Integrity and fairness | Deontology | No |
| 4 Reporting a Mistake | Christian Ethics | Honesty and responsibility | Virtue ethics | No |
| 5 Event Budget | Eastern Virtue Ethics | Honesty and accountability | Deontology | No |
| 6 Venue Agreement | Distributive Justice | Responsibility and honesty | Utilitarianism | No |

## Fields still owed

**Moments 1, 2, 4, 5, 6** (each):
1. Ethical Lens paragraph that explains how the assigned theory applies.
2. Theory link sentence that names the assigned theory.
3. Optional: the two Ethical Lens tag words, if they should change.
4. Optional, Moments 4 to 6 only: a TOPIC line like Moments 1 and 2 have.

**Moment 3 (CpEO leadership story, Aristotle's Virtue Ethics):**
1. Creative title
2. TOPIC line
3. Two Ethical Lens tag words
4. The Situation
5. The Ethical Conflict
6. The Ethical Lens
7. Theory link
8. My Decision
9. My Moral Insight

**Section 3 growth page (placeholders now in place):**
1. My Ethical Thinking
2. My Values
3. My Ethical Growth
4. The rest of "As a moral person, I commit myself to..."

## Other findings (not changed)

- **Real names of people:** none found in the journal text. Only the author's name appears. KodeKloud (a website) and LBC (a courier) are named.
- **Author name:** the page shows "JOHN BENEDICT C. PANTALLA", with the middle initial, in three places (meta author, closed cover, inside cover). The brief says "JOHN BENEDICT PANTALLA".
- **Em dashes in existing text:** three. Two are in Moment 1's Ethical Conflict ("permission, even due to an automatic system error, was"). One is in Moment 2's Theory link ("needs of others, especially when"). None were added.
- `ethically_me_journal_revised.docx` is not in the project folder.
