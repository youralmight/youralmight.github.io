# youralmight.github.io

This repository contains Yi Zhang's Quarto website and two DSCI 521 Milestone 3 computational posts. The posts analyze player countries, placements, and prize money from the Red Bull Wololo: Legacy 2022 Age of Empires IV tournament.

## Requirements

Install these tools before building the site:

- Git
- Quarto 1.10 or newer
- Python 3.14, managed through `uv`
- R 4.6.1 or compatible
- the R package `renv`

## Build from a clean clone

Run the shell commands from the repository root:

```bash
git clone git@github.com:youralmight/youralmight.github.io.git
cd youralmight.github.io
uv sync
Rscript -e 'renv::restore(prompt = FALSE)'
uv run quarto render
```

`uv sync` creates or restores the Python environment from `pyproject.toml`, `.python-version`, and `uv.lock`. `renv::restore()` restores the R packages listed in `renv.lock`. Run `quarto render` from the repository root so the project `.Rprofile` activates `renv`.

The rendered website is written to `docs/`. Open `docs/index.html` locally to inspect the generated site. The two Milestone 3 posts are:

- `posts/aoe4-r/index.qmd`
- `posts/aoe4-python/index.qmd`

## Data

The two CSV files in `data/` are:

- `player_profiles.csv`: player names and countries;
- `tournament_results.csv`: tournament placements and prize money.

The data are based on the [Esports Earnings page for Red Bull Wololo: Legacy 2022 – Age of Empires IV](https://www.esportsearnings.com/tournaments/56552-red-bull-wololo-legacy-2022-age-of-empires-iv). The source link is also included in both posts. The CSV files are committed locally, so rendering does not need network access to download the data.

The source's [Website Terms of Use](https://www.esportsearnings.com/terms-of-use) grant permission to use its materials for personal and commercial use. This repository contains only a small attributed extract of tabular facts and no source images, logos, or trademarks.

## GitHub Pages

GitHub Pages publishes the `docs/` directory from the `main` branch. After changing a QMD file or the data:

```bash
uv run quarto render
git status
git add .
git commit -m "describe the change"
git push origin main
```

The live website is published at <https://youralmight.github.io>.
