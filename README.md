# Predicting Electric Vehicle Purchases 🚗⚡

A collaborative machine learning project to analyze, explore, and predict electric vehicle purchase behavior.

---

## 📁 Repository Structure

```text
├── .github/workflows/     # CI/CD: Automated linting & notebook check
├── data/                  # Dataset files (train, test, sample submission)
├── model/                 # Model definitions, scripts, and checkpoints
├── notebook/              # Jupyter Notebooks for EDA and experiments
├── src/                   # Reusable data processing and utility modules
├── .gitattributes         # Line-ending normalization & notebook filters
├── .gitignore             # Ignores virtualenvs, caches, artifacts, checkpoints
├── .pre-commit-config.yaml# Git hooks (Ruff formatter, nbstripout, hygiene)
├── pyproject.toml         # Central tool configuration (Ruff) & project metadata
├── requirements.txt       # Core project dependencies
└── requirements-dev.txt   # Development, formatting, and linting tools
```

---

## 🛠️ Getting Started (Team Setup Guide)

To avoid formatting conflicts, notebook merge collisions, and "works on my machine" issues across operating systems (Windows, Mac, Linux), every team member should follow these steps:

### 1. Clone the repository
```bash
git clone https://github.com/3oFiz4/Predicting-Electric-Vehicle-Purchases.git
cd Predicting-Electric-Vehicle-Purchases
```

### 2. Create and activate a virtual environment
```bash
# Using python venv:
python -m venv .venv

# On Windows (PowerShell):
.venv\Scripts\Activate.ps1

# On Linux/macOS:
source .venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements-dev.txt
```

### 4. Enable pre-commit hooks (Crucial!)
```bash
pre-commit install
```
> **What this does:** Every time you run `git commit`, `pre-commit` will automatically:
> 1. Strip all execution outputs and cell execution counts from `.ipynb` files (`nbstripout`).
> 2. Format your Python scripts and notebook cells using **Ruff**.
> 3. Fix trailing whitespaces and normalize line endings.

---

## 🤝 Collaboration Best Practices

### Why Did Merge Conflicts Happen Before?
1. **Jupyter Notebook JSON bloat**: When you run a notebook, Jupyter saves your local execution count (`[1]`, `[2]`), execution timestamps, and output cells (including huge base64 images and logs). Even if two people edit different parts or just re-run the notebook, git sees conflict markers in the raw JSON and corrupts the file.
2. **Formatting differences**: Different editors format quotes, spaces, and line breaks differently. Modifying 1 line could trigger a 100-line reformatting diff.
3. **No line-ending normalization**: Windows uses `CRLF` while macOS/Linux uses `LF`.

### The Solution in This Repo
- **`nbstripout`**: Automatically strips cell outputs before committing, so only your actual code and markdown are tracked in Git.
- **`ruff`**: An ultra-fast Python linter and formatter that unifies style across `.py` and `.ipynb` files.
- **`src/` vs `notebook/` pattern**:
  - Keep notebooks clean and focused on **EDA, visualization, and storytelling**.
  - Extract reusable functions, data pipelines, and feature engineering logic into `src/` as pure Python modules (`.py`).
  - Import functions from `src/` into your notebooks instead of writing huge monolithic code blocks inside notebooks.

### Manual Commands
If you ever want to run checks manually:
```bash
# Check code style & linting:
ruff check .

# Automatically fix lint issues:
ruff check --fix .

# Auto-format all .py and .ipynb files:
ruff format .

# Manually strip outputs from all notebooks:
nbstripout notebook/*.ipynb
```
