# pythonProjects

A personal workspace for Python coursework and experiments. It is not a package — each
subdirectory stands on its own and can be opened directly in Jupyter or run with `python3`.

## Contents

| Path | What it is |
| --- | --- |
| [class asignmets/](class%20asignmets/) | Course assignments. Currently Week 1. |
| [class asignmets/Week 1 Assignment.ipynb](class%20asignmets/Week%201%20Assignment.ipynb) | First notebook: research topic notes (credit scores and microfinance in Latin America) plus intro Python cells. |
| [class asignmets/GDP.csv](class%20asignmets/GDP.csv) | Quarterly US GDP, `observation_date,GDP`, 1947-01-01 through 2026-04-01 (318 rows, billions of USD). FRED-style export. |
| [testAgentic/test1](testAgentic/test1) | Scratch file — a one-line `print("hello world")`. No extension; run it with `python3 testAgentic/test1`. |

## Setup

The system Python here is 3.9.6 with no third-party packages installed. Create a virtual
environment before adding any:

```sh
cd /Users/jhon/pythonProjects
python3 -m venv .venv
source .venv/bin/activate
pip install jupyterlab pandas matplotlib
```

## Running the notebook

```sh
source .venv/bin/activate
jupyter lab "class asignmets/Week 1 Assignment.ipynb"
```

Loading the GDP data from inside that notebook:

```python
import pandas as pd

gdp = pd.read_csv("GDP.csv", parse_dates=["observation_date"])
gdp.plot(x="observation_date", y="GDP")
```

Paths in the notebook are relative to the notebook's own directory, so `"GDP.csv"` is
correct when the kernel starts in `class asignmets/`.

## Known issue

In `Week 1 Assignment.ipynb`, the cell reading
`Do credit scores, would improve lifes in latam countries?` is a **code** cell, so running
the notebook top to bottom raises a `SyntaxError`. Switch it to Markdown (select the cell,
press `Esc` then `M`) before doing a full "Run All".

## Conventions

- Keep one directory per course or experiment.
- `.ipynb_checkpoints/` directories are Jupyter autosaves and can be deleted at any time.
- Data files live next to the notebook that uses them.
