# Biomolecule Toxicity Detective — Python edition

An investigation game about how toxic substances damage biomolecules, rebuilt entirely in
**Python**. You open four pieces of evidence, read a simulated dose–response dataset, and name
the damaged biomolecule and the mechanism. The biology is identical to the original website.
The website part is now Python (Streamlit) instead of HTML, CSS and JavaScript.

> **Educational simulation.** Every case, compound and number is simulated. Nothing here is a
> clinical, diagnostic or real-world toxicology assessment, and nothing describes how to obtain,
> prepare or handle any substance.

## What is inside

| Page | What you can do |
|---|---|
| Home | Briefing, the four biomolecule classes, scoring rules, case preview |
| Case Files | All six cases with difficulty and your progress |
| Investigation | Open evidence A–D, read the charts (Matplotlib, interactive, table, pattern detector), answer, use hints, get targeted feedback or the full explanation + causal pathway |
| Case Report | Score, case record table, mechanisms identified, download report (.txt / .csv) |
| Biomolecules | Database of DNA/RNA, proteins, lipids, carbohydrates |
| Toxin Library | 17 toxins, filter by category / target / text (Pandas), chart by target |
| Quiz | 10 questions, +10 points each |
| Mechanism Map | The 5 stages from exposure to effect |
| Cell Lab | Matplotlib drawing of the cell; trace the route of each mechanism |
| Python Lab (CT) | The four computational-thinking pillars shown with the project's real code |
| About | What the project is and is not |

Scoring: correct biomolecule **+50**, correct mechanism **+50**, solved first try with no hints
**+20**, each hint **−10**, each correct quiz answer **+10**.

## Run it on your computer

You need **Python 3.10 or newer** (python.org → Downloads; on Windows tick
*"Add python.exe to PATH"* during install).

**Easiest:** double-click `run.py`. The first time it installs the libraries, then it opens the site
in your browser at http://localhost:8501.

**Or with commands**, from inside this folder:

```bash
pip install -r requirements.txt
streamlit run app.py
```

(If `pip` or `streamlit` is "not recognised", use `python -m pip ...` and `python -m streamlit run app.py`.
On a Mac, type `python3` instead of `python`.)

**Terminal version (no installs at all):**

```bash
python play_in_terminal.py
```

**Run the automated tests:**

```bash
python -m unittest
```

## Put it online for free (Streamlit Community Cloud)

1. Create a new **public** repository on github.com (for example `btd-python`).
2. Click **Add file → Upload files** and drag in *everything inside this folder*, including the
   folders `btd`, `views`, `data`, `tests` and `.streamlit`. Click **Commit changes**.
   (On a Mac, press **Cmd + Shift + .** in Finder to show the hidden `.streamlit` folder so you can
   drag it. Without it the site still works, just with default colours.)
3. Go to **share.streamlit.io** and sign in with GitHub.
4. Click **Create app** → **"Yup, I have an app"**.
5. Fill in: **Repository** = your repo, **Branch** = `main`, **Main file path** = `app.py`.
   Optionally choose a custom **App URL**.
6. Click **Deploy**. After a few minutes you get a link like `https://your-name.streamlit.app`.

Free apps go to sleep after a while with no visitors; the first visitor clicks
"Yes, get this app back up" and it wakes in under a minute.

## How the project is organised

```
app.py                 front door: page setup, navigation bar, sidebar score
run.py                 one-click launcher
play_in_terminal.py    the same game with print() and input() only
requirements.txt       the four libraries
.streamlit/config.toml the pink theme (settings, not code)
data/                  the biology: cases, biomolecules, mechanisms, toxins, quiz (JSON)
btd/                   the engine — all the logic, no screens
    data.py            loads the JSON files                     (standard library)
    scoring.py         grade_case(), get_hint(), grade_quiz()   (standard library)
    progress.py        score, solved cases, text report         (standard library)
    analysis.py        trends, correlation, replicates, tables  (NumPy + Pandas)
    drawing.py         charts, cell diagram, flowcharts         (Matplotlib)
    ui.py              Streamlit helpers shared by the pages
views/                 one file per page of the website
tests/                 33 automated tests (unittest)
```

The website and the terminal game import the **same** `btd` engine, so a case can never be marked
differently in the two versions.

## Compared with the original website

| | Original website | Python edition |
|---|---|---|
| Languages written | JavaScript, HTML, CSS | Python only |
| Screens | React | Streamlit |
| Charts | hand-drawn SVG | Matplotlib (+ interactive Streamlit charts) |
| Server / API | Express REST API | Streamlit runs the Python on the server |
| Where the answer key lives | server (API mode) | server, always — never sent to the browser |
| Score saving | browser storage + API | this browser tab's session; download the report to keep it |
| Background animation | CSS + canvas | not included (Streamlit has no animation without CSS/JS) |
| Extra in this version | — | pattern detector, simulated replicates with error bars, Python Lab page, terminal edition |

See **PYTHON-GUIDE.md** for a walk-through of the code, the computational-thinking map and
likely viva questions.
