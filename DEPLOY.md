# ====================DEPLOY====================

This repository is **committed but not pushed**, and the GitHub repository has
**not been created**. Both need the account holder. This build was run with
`deploy only locally`, so the steps below are the remaining work rather than a
record of what happened.

---

## Run it locally first

From the working project (`D:\Claude_desktop\mid_range_org`):

```bash
python -m streamlit run public_repo/app/mid_range_org.py --server.port 8520
```

Or from inside `public_repo/`:

```bash
python -m streamlit run app/mid_range_org.py
```

The app finds its data at `data/mid_range_org_public.duckdb` when run from the
repository, and falls back to `public/mid_range_org_public.duckdb` when run from
the working project. Both paths are listed in `DB_CANDIDATES` at the top of the
app.

---

## Publish

**1. Create the GitHub repository.** Public, named `mid_range_org`, no README
(this repo already has one):

```bash
gh repo create mid_range_org --public --source=. --remote=origin --push
```

Or manually, then:

```bash
git remote add origin https://github.com/<account>/mid_range_org.git
git branch -M main
git push -u origin main
```

**2. Check the extract went with it.** `data/mid_range_org_public.duckdb` must be
in the commit and under GitHub's 50 MB warning threshold. It is not in
`.gitignore` — the `.gitignore` excludes `*.duckdb.wal`, which is the write-ahead
log and must never be committed, not the extract itself.

```bash
git ls-files -s data/ && du -h data/mid_range_org_public.duckdb
```

**3. Deploy on Streamlit Community Cloud.**

- Go to https://share.streamlit.io and choose **New app**
- Repository: `<account>/mid_range_org`
- Branch: `main`
- Main file path: `app/mid_range_org.py`
- **Custom subdomain: `celnic-mid-range-org`**

That gives `https://celnic-mid-range-org.streamlit.app/`.

Subdomains reject underscores, which is why the app slug is hyphenated
(`celnic-mid-range-org`) while the repository and database are snake_case
(`mid_range_org`).

**4. No secrets are needed.** The app reads a file in the repository and makes no
network calls. Nothing in `.streamlit/secrets.toml` is required, and the file is
gitignored in case one is added later.

---

## Refreshing the data

The published app reads whatever `data/mid_range_org_public.duckdb` contains, so
a refresh is a rebuild plus a push:

```bash
python scripts/run_all.py
cp public/mid_range_org_public.duckdb public_repo/data/
cd public_repo && git add -A && git commit -m "Refresh extract" && git push
```

Community Cloud hot-reloads on the push. **This works because `get_connection`
takes an extract fingerprint (path, size, mtime) as an argument** — Community
Cloud pulls the new files and re-runs the script but does *not* clear
`cache_resource`, so without the fingerprint a connection opened before the pull
would keep reading the replaced file and every refresh would need a manual
reboot. Do not remove that argument.

---

## Licence and attribution

The code is MIT. The data is New Zealand government open data under Creative
Commons Attribution licences — CC-BY 4.0, and CC-BY 3.0 NZ for the Charities
Register. Attribution per source is carried in the platform's own source register
and shown in the app's **Data & Provenance** tab.

Gazetteer attribution, required on the map tab and present there:

> Sourced from Toitū Te Whenua Land Information New Zealand data. Crown copyright
> reserved.

**This is not an official product of any New Zealand government agency**, and the
app says so in a banner above every tab.
