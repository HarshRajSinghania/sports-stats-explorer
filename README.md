# 🏀 Sports Stats Explorer

**A sports analytics dashboard that settles arguments with actual data.**

We're building a website that answers real questions about a sports league:
*Who are the best scorers? Which teams win close games? Is "clutch" even real?*

Along the way you'll learn **SQL** (joins and aggregation), **Python**, **charts**,
and **how to put a dashboard online**. No experience needed.

---

## How it works (the big picture)

```
 data/raw/*.csv  ──►  db/league.db  ──►  sql/*.sql  ──►  Python (pandas)  ──►  app/ (Streamlit + charts)
   raw stats         SQLite database     questions        DataFrames            the dashboard
```

1. **Data** — CSV files with teams, players, games and per-game stats (`data/raw/`).
2. **Database** — `scripts/load_data.py` loads the CSVs into a SQLite database.
3. **SQL** — each question we want to answer is one `.sql` file in `sql/`.
4. **Python** — `run_query("top_scorers", {...})` runs a SQL file and gives back a table.
5. **Dashboard** — each page in `app/pages/` turns one query into a chart.

> ⚠️ The data right now is a **fake league** (made by `scripts/generate_sample_data.py`)
> so we can start on day one. Swapping in a real league is on the roadmap.

---

## 🚀 Getting started

> **First time with Git/forks?** Read **[CONTRIBUTING.md](CONTRIBUTING.md)** first —
> it explains how to fork, clone, and keep your fork in sync with this repo.

You need **Python 3.10+** and **Git**.

```bash
# 1. Clone YOUR fork (replace <your-username>)
git clone https://github.com/<your-username>/sports-stats-explorer.git
cd sports-stats-explorer

# 2. Connect to the original repo so you can get updates
git remote add upstream https://github.com/data-science-ucsb/sports-stats-explorer.git

# 3. Make a virtual environment and install packages
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 4. Build the database
python scripts/load_data.py

# 5. Run the tests
pytest

# 6. Launch the dashboard (opens in your browser)
streamlit run app/Home.py
```

You should see the dashboard with a working **Top Scorers** page and three
🚧 pages waiting to be built.

---

## 📁 Project layout

```
sports-stats-explorer/
├── app/                        # The dashboard (Streamlit)
│   ├── Home.py                 #   landing page — run this
│   ├── common.py               #   shared helpers for pages
│   └── pages/                  #   one file = one page in the sidebar
│       ├── 1_Top_Scorers.py    #   ✅ worked example — copy this pattern
│       ├── 2_Standings.py      #   🚧 TODO
│       ├── 3_Close_Games.py    #   🚧 TODO
│       └── 4_Player_Profile.py #   🚧 TODO
├── sql/                        # One SQL file per question
│   ├── top_scorers.sql         #   ✅ worked example
│   ├── team_standings.sql      #   🚧 TODO (hints inside)
│   ├── close_games.sql         #   🚧 TODO (hints inside)
│   └── player_profile.sql      #   🚧 TODO (hints inside)
├── data/raw/                   # CSV data (one file per table)
├── db/schema.sql               # Table definitions — read this to learn the data!
├── scripts/
│   ├── generate_sample_data.py # makes the fake league
│   └── load_data.py            # CSVs → db/league.db
├── src/sports_stats/db.py      # run_query() and friends
├── tests/                      # pytest tests (TODO tests skip until you write the SQL)
├── ROADMAP.md                  # 👈 what to work on
└── CONTRIBUTING.md             # 👈 how to fork / sync / open a PR
```

---

## 🗄️ The data

Four tables. Open `db/schema.sql` for the details.

| Table | One row per… | Key columns |
|---|---|---|
| `teams` | team | `team_id`, `name`, `abbreviation` |
| `players` | player | `player_id`, `name`, `team_id`, `position` |
| `games` | game | `game_id`, `game_date`, `home_team_id`, `away_team_id`, `home_score`, `away_score` |
| `player_game_stats` | player per game | `game_id`, `player_id`, `team_id`, `minutes`, `points`, `rebounds`, `assists` |

**Try it:** explore the database directly with `sqlite3 db/league.db`, or install
the free [DB Browser for SQLite](https://sqlitebrowser.org/) app.

---

## 🧭 What do I work on?

See **[ROADMAP.md](ROADMAP.md)**. It's split into phases, starting with
beginner-friendly tasks. Each 🚧 TODO `.sql` file has hints at the top.

**The pattern for adding any new question to the dashboard:**

1. Write the SQL in `sql/<question>.sql` (test it in `sqlite3` first!)
2. Copy `app/pages/1_Top_Scorers.py` → `app/pages/N_Your_Page.py`
3. Change the query name, the inputs, and the chart
4. Add a test in `tests/test_queries.py`

---

## 📚 Learning resources

| Topic | Resource |
|---|---|
| SQL basics | [SQLBolt](https://sqlbolt.com/) (interactive, ~1 hr) |
| SQL joins / GROUP BY | [Mode SQL Tutorial](https://mode.com/sql-tutorial/) |
| Python | [Python for Everybody](https://www.py4e.com/) |
| pandas | [10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html) |
| Charts | [Plotly Express](https://plotly.com/python/plotly-express/) |
| Dashboard | [Streamlit docs](https://docs.streamlit.io/) · [Cheat sheet](https://docs.streamlit.io/develop/quick-reference/cheat-sheet) |
| Git | [Git & GitHub for Beginners (freeCodeCamp)](https://www.youtube.com/watch?v=RGOj5yH7evk) |
