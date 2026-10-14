# Roadmap

Tasks are grouped into phases. **Pick something, claim it (comment on the issue or
tell the group), branch, build it, open a PR.** See [CONTRIBUTING.md](CONTRIBUTING.md)
for the Git steps.

Difficulty: 🟢 beginner · 🟡 intermediate · 🔴 stretch

---

## Phase 0 — Get set up (everyone)

- [ ] 🟢 Fork, clone, add `upstream`, and pull the starter code (CONTRIBUTING.md)
- [ ] 🟢 Install packages, run `python scripts/load_data.py`, `pytest`, and `streamlit run app/Home.py`
- [ ] 🟢 Read `db/schema.sql`, then open the database (`sqlite3 db/league.db`) and try:
      `SELECT * FROM games LIMIT 5;`
- [ ] 🟢 Read `sql/top_scorers.sql` and `app/pages/1_Top_Scorers.py` line by line.
      This is the pattern for everything else.

## Phase 1 — Answer the core questions (SQL + charts)

Each one = write the `.sql` file (hints inside) → its test in `tests/` stops
skipping and starts running → add a chart to the page.

- [ ] 🟢 **League summary** — move the headline-numbers query in `app/Home.py` into `sql/league_summary.sql`
- [ ] 🟡 **Standings** — `sql/team_standings.sql` + chart on `app/pages/2_Standings.py`
- [ ] 🟡 **Close games** — `sql/close_games.sql` + chart on `app/pages/3_Close_Games.py`
- [ ] 🟡 **Player profile** — `sql/player_profile.sql` + line chart; replace the text box with a player dropdown
- [ ] 🟢 **More leaderboards** — rebounds and assists leaders (copy the Top Scorers pattern, or add a stat dropdown to it)

## Phase 2 — Real data

The fake league is just training wheels.

- [ ] 🟡 **Choose a league** as a group. Options:
  - NBA via the [`nba_api`](https://github.com/swar/nba_api) Python package
  - WNBA / NBA / NFL datasets from [Kaggle](https://www.kaggle.com/datasets?search=nba)
  - Soccer: [football-data.co.uk](https://www.football-data.co.uk/data.php) CSVs
  - Any other league you care about — UCSB teams, anyone?
- [ ] 🟡 Write `scripts/fetch_real_data.py` that downloads + cleans the data into CSVs
      **in the same shape** as `data/raw/` (see `data/README.md`)
- [ ] 🟡 Update `db/schema.sql` if the real data has extra useful columns (e.g. 3-pointers, fouls)
- [ ] 🟢 Update the tests that assume 8 teams

## Phase 3 — Settle more arguments

Come up with your own! Some ideas:

- [ ] 🟡 **Home-court advantage** — do teams really win more at home?
- [ ] 🟡 **Hot streaks** — longest winning streak per team (look up SQL *window functions*)
- [ ] 🟡 **Head-to-head** — pick two teams, show every game between them
- [ ] 🟡 **Compare two players** — side-by-side stats
- [ ] 🔴 **Efficiency** — points per minute; who's underrated (high efficiency, low minutes)?
- [ ] 🔴 **Is "clutch" real?** — do teams that win close games keep winning them, or is it luck?

## Phase 4 — Put it online 🌐

- [ ] 🟢 Deploy to [Streamlit Community Cloud](https://streamlit.io/cloud) (free):
      sign in with GitHub → **New app** → repo `data-science-ucsb/sports-stats-explorer`,
      branch `main`, main file `app/Home.py`. The app builds the database itself on first load.
- [ ] 🟢 Add the live link to the top of the README
- [ ] 🟡 Polish: consistent colors, team logos, a nicer home page

---

### Have an idea that isn't here?
Open an issue using the **Task** template and bring it up at the next meeting.
