# Brand Wars — shared-team investment cycles

## Quick preview

Open `index.html` → **Instructor dashboard** → enter **glhf**. Choose **Demo · 6 automated rivals**. Use **Start stage** or **Finish briefing** to begin. Six simulated brands choose automatically in every round.

Student screens choose **Join as a team** and enter a number from **1 to 15**. Anyone entering the same number shares that team's selections. Team numbers stay joined when you reset. In offline mode this sharing works between pages in the same browser storage; separate student devices need live mode.

## The simplified activity

First, teams choose a brand name and an Everyday, Performance or Style promise. Then six investment cycles use the **same four areas**:

- Product design: improve the core benefit; make fit and use easier.
- Brand identity: build recognizable cues; make the benefit understandable.
- Product experience: make the promise dependable; help customers use and care for it.
- Brand growth: develop a close extension; adapt for a new customer segment.

All eight methods are visible on one page, in four separate boxes. Teams may combine methods across areas. Each card explains the concrete work, what customers notice, and the tradeoff. No numerical future BAV changes are exposed.

Each cycle has 25 credits. Allocate in steps of 5, with at most 15 per method and at most four funded methods. One funded method is a valid partial portfolio. Unspent credits expire. Repeating the same method adds progressively less incremental value.

## Automatic saving — no lock button

Each change is saved to the shared team immediately. Teammates see the same allocation. The status shows Saving or saved. Choices remain editable until the stage closes; there is no separate lock or submission step.

When decision time ends—or the instructor closes early—the instructor scores the **last saved selections**. A partially spent budget is scored. An entirely empty portfolio earns no new equity. Both a name and a promise are needed to initialize a brand. The naming screen explicitly prompts for either missing selection.

Live changes require a connection and server acknowledgement. The saved indicator distinguishes completed saves from pending changes; the game does not claim that an unacknowledged network change has reached the shared session. A pending change arriving after reset or stage closure is rejected rather than applied to the wrong stage.

## Teacher controls and timing

- **Start stage:** opens decisions and starts the countdown.
- **Close stage & report:** freezes the latest saved choices, publishes the report and starts its separate countdown.
- **Pause / Resume:** pauses either phase and prevents decision changes while paused.
- Decision expiry opens the report automatically. Report expiry opens the next decision stage automatically.
- During a report, **Start next stage** advances early.
- **Reset session:** clears scores, names, promises and allocations across all currently open screens. Registered team numbers remain joined. Old in-flight edits cannot restore pre-reset choices. Demo resets recreate the six rivals.

Keep one instructor page open and connected for automatic transitions. The countdown uses an absolute deadline rather than decrementing a local counter. If the instructor device is asleep, progression resumes when the page runs again.

| Stage | Decision / activity | Report | Total |
|---|---:|---:|---:|
| Briefing | 5 min | — | 5 min |
| Name & promise | 5 min | 2 min | 7 min |
| Build the foundation | 7 min | 2 min | 9 min |
| Become understood | 7 min | 2 min | 9 min |
| Earn repeat use | 7 min | 2 min | 9 min |
| New occasions | 7 min | 2 min | 9 min |
| New customers | 7 min | 2 min | 9 min |
| Defend or expand | 7 min | 2 min | 9 min |
| Final debrief | 9 min | — | 9 min |
| **Total** | | | **75 min** |

Demo uses 2-minute decisions and 1-minute reports, plus a 3-minute briefing and final debrief. Pauses and early advancement change elapsed class time.

## Knowledge and Esteem

**Knowledge** is familiarity and understanding: do people recognize the brand and know what it stands for? Consistent brand cues, clear explanations and usable product guidance can help.

**Esteem** is respect, perceived quality and trust: do people regard the brand as good and credible? Testing, dependable quality and delivery of the promise can help.

Reports include a Knowledge-versus-Esteem chart, exact comparisons across teams, interpretations and definitions of all four pillars. Brief strategy reviews describe observed capability gaps, fit, competitor overlap and diminishing returns without questions or prescribed allocations. The total-value formula appears beside team scores.

## Naming fit

Each team has six exclusive names with stated associations; no other team can choose them. All teams have two names aligned with each of the three promises. This is intentional: scoring freely typed names with a keyword guess would be unreliable. A predefined mismatch deducts 0–0.5 Knowledge at the first report. The same association/position combination receives the same treatment for every team. The instructor guide shows the complete naming key; the report explains any penalty.

All positions have a $210M base before naming fit. A neutral or aligned name preserves that base. Names are not proof of product quality and receive no automatic bonus.

## Final report and scoring

The final report compares realized class strategies and examines all **1,158 legal single-round portfolios** for each team, holding its actual prior history and rivals' actual commitments fixed. It shows specific allocation differences, possible improvement that round, and naming fit. Separate round gains must not be added: changing earlier decisions changes later capabilities. This is not a globally optimized full-game strategy.

Value remains `(D + R) × (E + K) × $5M`. Maximum Strength is 16 and Stature 15, so value cannot exceed $1.20B. Fit, capability support, competitive overlap, concentration and repeated-investment discounts affect returns. Identity earns less Esteem without product evidence. Reports are model-generated, not customer survey findings.

## Live shared-team setup

The supplied HTML already contains the public Firebase configuration from your original game. This version uses a **new `brandwarsExpansion/SESSION` branch** because editable shared teams require different rules. Earlier `cdj`, `brandwars` and `brandwarsProduct` sessions are not modified.

1. In Firebase Authentication, copy the instructor account UID. Anonymous and Email/Password sign-in must be enabled.
2. Replace `PASTE_INSTRUCTOR_UID` in the supplied `database.rules.json` with that UID.
3. Merge the supplied **brandwarsExpansion** branch into the existing top-level `rules` object in Realtime Database. Preserve every existing game branch. Publish the merged rules.
4. Host the updated `index.html` on your static host.
5. Open the hosted page, choose a session name and click **Open live classroom**. Share the exact resulting `?session=CLASS-NAME&live=1` link.
6. Teacher: enter **glhf**, then the existing Firebase instructor account details if not already signed in. Students: enter their team number, then choose name and promise when that stage opens.

`glhf` is a simple classroom entry gate. The Firebase instructor account remains necessary to authorize live timer, report and reset writes; a password embedded in a downloadable HTML file is not server authentication. Students sign in anonymously in the background. Anyone in the class can join any numbered team, as requested, so students should use their assigned number.

The rules allow same-team edits only for the currently open, running stage and current reset generation. Teacher writes control game state and published reports. Reset changes the generation so delayed old edits fail.

## Verification and deployment status

Local browser tests covered the password gate, two pages joining one team, simultaneous updates combining correctly, autosave at time expiry, partial portfolio scoring, naming penalties, Knowledge/Esteem reporting, mobile layout, reload recovery and resetting while student pages remain open. Stale writes after reset were rejected. The full demo reaches final comparisons.

Scoring tests covered all **20,844 promise/round/portfolio combinations** (3 × 6 × 1,158) along sampled histories, plus 50 histories with exhaustive final comparisons. Scores stayed finite and did not exceed $1.20B. Growth appeared in the strongest late-round mix in 34 of the 50 sampled histories. Every team has six unique names and equally balanced naming-fit options. Browser checks covered the full six-round flow, exclusive-name rejection, 75-minute timing and layouts at 390, 768 and 1280 pixels.

The updated Firebase client and rules are included, but have not been deployed or tested against your live project. Publishing the rules and hosting the file remain setup steps. Test with an instructor and two student devices before class.


## Six-cycle edition
Replace the HTML and install the accompanying database rules (namespace `brandwarsExpansion`). Existing older sessions are separate. Each numbered team owns six names; other teams cannot select them. Demo rivals have their own names.

75-minute pacing: briefing 5; name/promise 5 + report 2; six investment rounds 7 + report 2 each; final debrief 9. All eight methods appear together. New-market and product-extension opportunities become more receptive in later rounds.
