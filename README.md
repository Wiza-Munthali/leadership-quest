# Leadership Quest

A gamified study companion for the **Africa Leadership Accelerator (ALA) 2026–27** fellowship. It turns the 13 sessions from the first convening in Zambia into a road trip: each session is a roadside stop where you read the idea in plain language, flip through the key frameworks, take on a scenario challenge, and write down a commitment to bring to your pod.

The design is inspired by the hand-painted shop and barbershop signs found across Malawi and Zambia.

> An unofficial learning aid made by a fellow, for fellows. It is not a Global Health Corps product.

---

## What's inside

**13 stations in 4 camps**

| Camp | Stations |
|---|---|
| 1 · Know yourself | Authentic Leadership & Mindtraps · Vision, Values & Human-Centred Design · Self-Trust & Self-Compassion · Story of Self |
| 2 · Lead with others | Collective Leadership · Negotiating Relationships (Five Core Concerns) · Roles in Social Change |
| 3 · Work well together | Giving & Receiving Feedback · Mental Health & Psychological Safety · Cohort Check-In (20 Experiences) · Managing Up, Down & Across |
| 4 · From story to action | Story of Us & Now · The Science of Goal Setting |

**Every station has five steps**

1. **In plain words**: the session in a few sentences, plus a one-line "Remember" hook
2. **Flip the cards**: each framework on a card, with a question to ask yourself on the back
3. **The case**: the scenario used in the session (Peter and Nandi, Amani, Amina and others)
4. **Challenge**: multiple-choice, match-the-pairs and put-in-order questions, each with a short explanation
5. **Your move**: the session's commitment prompt, saved privately in your browser

**Game features**

- XP and ranks: Newcomer → Listener → Experimenter → Builder → Weaver → Guide → Visionary
- Up to three stars per station, based on how many answers you get right first time
- A road that turns from dirt to tarmac as you clear stations
- 13 badges and a daily streak
- **Rapid Fire**: a 60-second quiz drawing on all 13 sessions
- **Cheat Sheet**: every framework on one searchable page
- **Progress**: your badges plus all your commitments, with a copy button so you can paste them into pod check-ins or your *Why I Lead* draft

---

## Using it

Open the site on a phone or computer and start at the first stop. You don't need an account.

**Your progress stays on your device.** XP, stars, badges and commitments are stored in your browser's local storage. Nothing is sent anywhere, so:

- nobody else can see your progress or your commitments
- progress doesn't follow you to another device or browser
- clearing your browser data (or using a private window) starts you over

Use **Progress → Reset progress** to start again on purpose.

---

## Running it locally

The whole app is one self-contained file, `index.html`. It has no build step, framework or dependencies. The only external resources are the Google Fonts it loads (Bungee and Archivo); without a connection it falls back to system fonts.

```bash
# Option 1: just open the file
open index.html

# Option 2: serve it (closer to how it behaves when hosted)
python3 -m http.server 8000
# then visit http://localhost:8000
```

---

## Deploying

### GitHub Pages

1. Push `index.html` (and this README) to a **public** repository.
2. Go to **Settings → Pages**.
3. Under *Build and deployment*, choose **Deploy from a branch**, then select `main` and `/ (root)`.
4. The site goes live at `https://<username>.github.io/<repo-name>/` within a minute or two.

### Netlify or Vercel

- **Netlify Drop:** drag the folder onto app.netlify.com/drop, then sign in so the site isn't removed.
- **Vercel:** run `npx vercel` in the project folder.

---

## Editing the content

All content lives in the `<script>` block of `index.html`, in two constants.

**`ARCS`** lists the four camps (name and subtitle).

**`S`** lists the 13 stations. Each station looks like this:

```js
{
  id: 1, arc: 0,                 // station number, camp index (0–3)
  short: "Mindtraps",            // label on the trail
  title: "Authentic Leadership: Mindsets & Mindtraps",
  plain: "…",                    // Step 1, plain-language summary
  hook:  "…",                    // the "Remember" line
  src:   "…",                    // source / attribution line
  cards: [{ k: "Rightness", d: "…", q: "What evidence could change my view?" }],
  cs:    { name: "…", text: "…" },   // the case from the session
  quiz:  [ /* see below */ ],
  move:  { prompt: "…", f: ["Field 1", "Field 2", "Field 3"] }
}
```

**Question types**

```js
// Multiple choice: `a` is the index of the correct option (options are shuffled on screen)
{ t: "mcq", q: "Question?", o: ["Right", "Wrong", "Wrong"], a: 0, w: "Why it's right" }

// Match the pairs: write each pair correctly; the right-hand column is shuffled on screen
{ t: "match", q: "Match…", p: [["Term", "Meaning"], ["Term", "Meaning"]], w: "…" }

// Put in order: list the items in the correct order; they are shuffled on screen
{ t: "order", q: "Put in order…", i: ["First", "Second", "Third"], w: "…" }
```

Match questions support up to six pairs. Rapid Fire draws on every multiple-choice question that has three or more options.

To adapt the app for a later convening, replace the entries in `S` (and `ARCS` if the camps change). The trail, scoring and badges adjust automatically. Badges that point at specific stations (Trap Spotter → station 1; Storyteller → stations 4 and 12) are defined in `checkBadges()`.

> **Note:** progress is stored under the key `alaQuest.v1`. If you change the stations significantly, rename the key (for example to `alaQuest.v2`) so returning players start fresh instead of carrying over mismatched progress.

---

## Credits and sources

The content summarises the ALA 2026–27 first-convening session materials and the frameworks they draw on:

- **Mindtraps**: Jennifer Garvey Berger, *Unlocking Leadership Mindtraps* (2019)
- **Human-Centred Design**: IDEO.org
- **Self-compassion**: Kristin Neff
- **Story of Self / Us / Now**: Marshall Ganz (public narrative), plus the *Truth Be Told* six-step framework
- **Collective leadership**: WHO/Alliance, *Open Mindsets: Participatory Leadership for Health*
- **Five Core Concerns**: Roger Fisher & Daniel Shapiro, Harvard Negotiation Project
- **Social Change Ecosystem**: Deepa Iyer / Building Movement Project
- **Feedback triggers & switchtracking**: Douglas Stone & Sheila Heen, *Thanks for the Feedback*
- **Mental health & psychological safety session**: facilitated by Kalunga Chalungumana (StrongMinds Zambia, GHC alum), using DISC styles
- **MOCHA, check-ins, One-Minute email**: The Management Center
- **Goal setting**: Locke & Latham (2002); if–then planning: Gollwitzer & Sheeran

The case studies (Peter and Nandi, Amani, Amina and others) are the fictional scenarios used in the sessions. All framework summaries are paraphrased for study purposes. For the full ideas, go to the original sources and session materials.

---

Built by Wiza, ALA 2026–27 fellow, with Claude.