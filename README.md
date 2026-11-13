# Change in Condition Charting Lab

An interactive, Cerner PowerChart–style practice lab. Bedside nurses notice a change in condition, assess, escalate, and document a focused assessment and their communication. One self-contained HTML file (`index.html`) with no build step, no server and no login. Nothing a learner enters is saved or sent.

**Training environment only.** Patients, data and times are fictional. Clinical content is for practice and is pending SME validation (see below).

## Cases

Each case has a non-ICU version (A) and an ICU version (B).

| # | Case | Core lesson |
|---|------|-------------|
| 1 | Respiratory decline | Count the RR yourself. Chart oxygen device and flow with every SpO2. |
| 2 | Hypotension | A low BP charted with no record of who was told isn't a plan. Go around an unanswered page. |
| 3 | Stroke / TIA | "Neuro unchanged" isn't a baseline. Last known well needs a witness. Don't stand down when symptoms improve. |
| 4 | Abdominal pain with N/V/D | "GI upset, Zofran given" isn't an abdominal assessment. Measure losses. Reassess. |
| 5 | Delirium vs withdrawal | "Confused" isn't a finding. Test attention, find contributors, keep withdrawal on the differential. Calm isn't cleared. |
| 6 | GI bleed, deteriorating | Hemoglobin lags. Escalate again on recurrence. A transfer order isn't a handoff. |

Escalation routes:
- Non-ICU: primary/cross-cover hospitalist, then RRT per CP5-105. Stroke activation goes through the RRT.
- ICU: resident/APP, then fellow, then attending, plus the specialty that owns the device. Stroke activation goes through the ICU team.

## How it works

- **Layout:** chart menu, then the story panel, then the chart.
- **Story panel:** the panel on the left of the chart holds the scenario as an accordion by stage. The current step is open, and its next button is pinned to the bottom. Finished stages collapse and can be reopened for review.
- **Chart:** the chart behaves like PowerChart (Nurse View, IView/I and O, eMAR, Results, Orders, Documents). It never changes screens by itself. When the story needs a screen, that menu item glows.
- **Charting:** bedside findings become tap-to-chart values, one line per IView row. A row with conflicting sources (e.g., monitor RR vs counted RR) lets the learner pick one. Calls chart into Communication Information with one button. Handoff uses dropdowns (you as giver, the receiving nurse) and pick lists with distractors.
- **Monitor data in ICU cases:** the ICU charting column arrives with monitor data in purple. Signing validates it.
- **Learner modes:** New / newly hired (guidance at every step plus a "what this entry needs" checklist), Experienced (guidance on request), Charge / RRT.
- **First run:** a six-step guided tour on first launch. The **Tour** button replays it.
- **Debrief:** tabs for Summary, Your actions, Score detail, Your chart (auditor view), and Answer key. Safety flags are listed for educator follow-up regardless of score.

## Educator settings

- **Pass mark:** add `?pass=80` to the URL to show a pass mark in the debrief. With no parameter, the debrief says passing standards are set by the educator.
- **Score:** the score is formative, out of 100. It covers recognition, escalation, documentation, reassessment, and handoff.

## Deploy (GitHub Pages)

Settings → Pages → Deploy from a branch → `main` / root. The lab will be at `https://scottbrickner.github.io/change-in-condition-lab/`.

Layout is tested at 1280×720 (unit workstations), 1024×768 and 1440×900. Phones aren't supported.

## Tests

`tests/run-cases.js` plays every version end to end with Playwright: best paths, trap paths, and chips-only charting. It prints each rubric score and any safety flags. Best paths should score 100.

```
npm i playwright && npx playwright install chromium
node tests/run-cases.js            # all
node tests/run-cases.js c3         # just Case 3
```

## Pending SME / local validation

Do not use with learners until these are confirmed:

- Every dose and order in the cases, including:
  - furosemide
  - NS/LR boluses
  - norepinephrine start and notify thresholds, and peripheral norepinephrine
  - epidural rate change
  - lorazepam
  - thiamine
  - PRBC, MTP and transfusion vital-sign timing
- Oxygen protocols:
  - floor NC up to 4 L
  - ICU up to 6 L
- CP5-105 RRT criteria wording, the "dial 77" route, and the 10-minute rules
- Neuro-check frequency after stroke activation
- Choice of delirium tool (4AT / bCAM / CAM-ICU) and the withdrawal assessment pathway
- Contact enteric precautions and C. difficile testing criteria
- Who can pause tube feeds (order vs protocol); gastric residual checks
- Straight-cath threshold (> 500 mL)

