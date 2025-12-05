# USPTO CBSA patents — Data prep

This repository contains a Jupyter notebook `test.ipynb` that scrapes USPTO CBSA patent counts (2015), normalizes names against the Census gazetteer, and produces a Datawrapper-ready CSV `datawrapper_cleaned.csv`.

## Quick start

1. Activate the project's virtual environment:

```bash
source .venv/bin/activate
```

2. Install dependencies (recommended):

```bash
pip install -r requirements.txt
```

3. Run the notebook interactively (recommended) using VS Code or Jupyter, or execute top-to-bottom non-interactively:

```bash
python -m nbconvert --to notebook --execute test.ipynb --inplace
```

After running, the final output `datawrapper_cleaned.csv` will be written by the last notebook cell.

## Notes

- The `.venv/` directory is ignored by `.gitignore` — do not commit your virtual environment.
- Large intermediate CSVs and raw data are ignored; the notebook was adjusted to keep intermediate data in-memory and only write the final CSV.

## CI

A GitHub Actions workflow (in `.github/workflows/ci.yml`) is included that will run the notebook on push.

## License

Pick a license for your repo and add `LICENSE` if you plan to make this public.
