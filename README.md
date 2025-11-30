**Bank Reviews Scraper & Preprocessing**

**Overview:**
- **Project:** Scrape Google Play Store reviews for Ethiopian banks, clean and preprocess them for analysis.
- **Components:** A scraper (`scraper.py`) that collects reviews and app metadata; a preprocessor (`preprocessing.py`) that cleans and prepares the data; a config file (`config.py`) for IDs, names and file paths; and an exploratory notebook (`preprocessing_EDA.ipynb`).

**Files of interest:**
- `scraper.py`: Main Google Play reviews scraper (class `PlayStoreScraper`).
- `preprocessing.py`: `ReviewPreprocessor` class for cleaning and transforming raw reviews.
- `config.py`: App IDs, bank names, scraping settings and data paths.
- `preprocessing_EDA.ipynb`: Notebook combining scraping, preprocessing and visualizations.
- `data/raw/` and `data/processed/`: Default locations for raw and processed CSVs (see `config.py`).

**Quick Setup (Windows / PowerShell)**
- Create and activate a virtual environment (recommended):
  ```powershell
  cd 'C:\Users\ZAK-TECH\Desktop\KAIM week 2\week_1'
  python -m venv .venv
  & .venv\Scripts\Activate.ps1
  ```
- Install dependencies (project has a `requirements.txt`):
  ```powershell
  pip install -r requirements.txt
  ```
- If you use GitHub Actions or CI that needs secrets, add them to your environment or `.env` file. The project uses `python-dotenv` to load values from `.env`.

**Configuration**
- Edit `config.py` or set environment variables to override defaults:
  - `CBE_APP_ID`, `BOA_APP_ID`, `DASHEN_APP_ID` — App package names.
  - `REVIEWS_PER_BANK` — Number of reviews to attempt to fetch per bank.
  - `MAX_RETRIES` — Retry attempts for network errors.
- Data paths are defined under `DATA_PATHS` in `config.py` (raw/processed CSV paths).

**Run the Scraper**
- Run the scraper module directly (from the `Scraper` folder or repo root):
  ```powershell
  & "C:/Users/ZAK-TECH/Desktop/KAIM week 2/.venv/Scripts/python.exe" "c:/Users/ZAK-TECH/Desktop/KAIM week 2/week_1/Scraper/scraper.py"
  ```
- The scraper will:
  - Fetch app metadata and save `app_info.csv` to the raw data folder.
  - Scrape reviews for each bank and save them to `data/raw/reviews_raw.csv`.

**Run Preprocessing**
- You can run preprocessing as a script to read raw CSV and produce processed CSV:
  ```powershell
  & .venv\Scripts\python.exe c:\Users\ZAK-TECH\Desktop\KAIM week 2\week_1\Scraper\preprocessing.py
  ```
- Or run the notebook `preprocessing_EDA.ipynb` in Jupyter / VSCode to execute scraping + preprocess + visualize.

**Notebook usage**
- Open `preprocessing_EDA.ipynb` in Jupyter or VS Code and execute cells in order.
- The import cell reloads `scraper` to ensure recent edits are used by the running kernel (avoids stale module caching).

**Notes & Troubleshooting**
- KeyError for bank codes (e.g. `'BOA'`) often means a mismatch between `bank_code` values and keys in `BANK_NAMES` or `APP_IDS` (case/whitespace differences). The scraper includes normalization (strip + upper) to avoid this. If you still see problems:
  - Print the mappings and scraped bank codes before processing (use `repr()` to reveal hidden chars).
  - In the notebook, reload the `scraper` module after edits using `importlib.reload(scraper)`.
- If you change remote data paths in `config.py`, ensure those folders exist or the code will attempt to create them.

**Suggested next steps**
- Normalize `bank_code` in preprocessing on load (recommended) — this helps if raw CSV contains variant codes.
- Add unit tests for edge cases (missing bank names, unexpected review schema).

**Contact / Contributing**
- If you make changes, run the notebook end-to-end and check `data/processed/reviews_processed.csv`.
- Open issues or PRs with sample failing rows if you hit unexpected errors.

**License**
- This repository does not include an explicit license file. Add one if you plan to share publicly.

---
Generated from `scraper.py`, `preprocessing.py`, `config.py` and `preprocessing_EDA.ipynb` in this folder.
