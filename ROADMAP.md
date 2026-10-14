# Roadmap

This page shows what we will build, one workshop at a time.

**You do not need to read all of this today.** Find the workshop you are on, read that section, and ignore the rest until you get there.

---

## How this works

Each workshop has three parts:

1. **In the workshop** you learn one skill, like SQL or making charts.
2. **By the end of the workshop** you will have finished something small and real.
3. **The take-home** uses that same skill on the actual project code. It should take about an hour.

Every take-home has two levels. **Pick one:**

- **Starter:** the main task. Doing just this is plenty.
- **Challenge:** optional, for when you finish the Starter and want more.

Missed a workshop or fell behind? That's fine. Each take-home works on its own, so you can skip ahead and come back later.

---

## The plan at a glance

| Workshop | You will learn | By the end you will have | Take-home |
|---|---|---|---|
| 1. Setup and Git | Forks, cloning, running the project | The dashboard running on your laptop | Make your first pull request |
| 2. SQL basics | `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY`, `COUNT`, `SUM`, `AVG` | Your own queries running on the league database | Write a leaderboard query |
| 3. SQL joins | `JOIN`, `CASE WHEN` | Queries that combine teams, players, and games | Build the Player Profile query |
| 4. Python and charts | pandas, Plotly, Streamlit pages | A chart on the dashboard that you made | Add a chart to a dashboard page |
| 5. Going live | Deploying, picking your own question | The dashboard online with a real link | Answer a question of your own |

Workshop leads may change the order or the dates. This table is the plan, not a promise.

---

## Workshop 1: Setup and Git

**In the workshop:** fork the repo, download it to your laptop, install everything, and start the dashboard. We will also cover how Git, forks, and pull requests fit together.

**By the end you will have:**
- The dashboard running on your laptop with `streamlit run app/Home.py`
- The `upstream` remote set up, so you can download new code from the club repo

The setup steps are in the [README](README.md#getting-started). The Git steps are in [CONTRIBUTING.md](CONTRIBUTING.md).

### Take-home 1: Make your first pull request

You will practice the full Git workflow on something that can't break anything.

**Starter**

1. Make a branch: `git checkout -b add-<your-name>`
2. Create a file called `members/<your-github-username>.md`
3. Write in it your name, your year or major, and your favorite team or sport
4. Commit it, push it to your fork, and open a pull request to the club repo

**Done when:** your pull request is open on GitHub.

**Challenge**

Open the database with `sqlite3 db/league.db` and find:
- How many games are in the database? (`SELECT COUNT(*) FROM games;`)
- What were the scores of the first five games?
- Which players are on team 1?

<details>
<summary>Stuck?</summary>

- "Permission denied" when pushing? Make sure you push to `origin` (your fork), not `upstream`.
- Not sure your pull request went to the right place? It should say `base: data-science-ucsb/main`.
- Step-by-step Git help is in [CONTRIBUTING.md](CONTRIBUTING.md).
</details>

---

## Workshop 2: SQL basics

**In the workshop:** ask the database questions about one table at a time. Filter rows, sort them, and add them up.

**By the end you will have:**
- Written your own queries in `sqlite3`
- Read through `sql/top_scorers.sql` and understood each line

### Take-home 2: Write a leaderboard query

The dashboard has a Top Scorers page. Make one for another stat.

**How the workshop helps:** `GROUP BY` puts each player's games together, `AVG()` turns them into a per-game number, and `ORDER BY ... DESC` puts the best player first. That's the whole query.

**Starter**

1. Copy `sql/top_scorers.sql` to a new file, `sql/top_rebounders.sql`
2. Change it to use `rebounds` instead of `points`
3. Test it in `sqlite3`. The `:limit` and `:min_games` placeholders need values first:
   ```
   sqlite3 db/league.db
   .param set :limit 10
   .param set :min_games 5
   .read sql/top_rebounders.sql
   ```

**Done when:** the query lists the 10 best rebounders, highest first.

**Challenge**

`app/Home.py` has a query written directly in Python (look for the `TODO` comment). Move it into a new file, `sql/league_summary.sql`, and change `Home.py` to use `run_query("league_summary")`, the same way the Top Scorers page does.

<details>
<summary>Stuck?</summary>

- Every column in `SELECT` must be either in the `GROUP BY` or inside a function like `SUM()` or `AVG()`.
- `HAVING` is like `WHERE`, but it filters after grouping.
- Try [SQLBolt lessons 1 to 4 and 10 to 12](https://sqlbolt.com/).
</details>

---

## Workshop 3: SQL joins

**In the workshop:** combine tables with `JOIN`, and use `CASE WHEN` to make decisions inside a query, like "was this a win or a loss?"

**By the end you will have:**
- Written a query that joins two or more tables
- Understood how the ID columns connect the tables (see [The data](README.md#the-data) in the README)

### Take-home 3: Build the Player Profile query

**How the workshop helps:** a player's game log needs four tables. `JOIN` connects them, and `CASE WHEN` works out who the opponent was.

**Starter**

1. Open `sql/player_profile.sql` and read the hints at the top
2. Write the query below the hints
3. Run `pytest`. The `test_player_profile` test will stop skipping and start checking your work.

**Done when:** `pytest` passes, and the Player Profile page shows a table when you type in a player's name.

**Challenge**

Write `sql/team_standings.sql` (hints inside). It's harder because every game involves two teams. The hints show a trick for handling that.

<details>
<summary>Stuck?</summary>

- Start small. Join just `player_game_stats` and `players` and check that the output looks right, then add one table at a time.
- To find a player's name to test with, run `SELECT name FROM players LIMIT 5;`
- If you get way too many rows, a `JOIN ... ON` condition is probably missing or wrong.
</details>

---

## Workshop 4: Python and charts

**In the workshop:** load query results into pandas, make charts with Plotly, and see how a Streamlit page fits together.

**By the end you will have:**
- Read through `app/pages/1_Top_Scorers.py` and understood its three parts: inputs, query, and chart
- Made a chart in Python from a query result

### Take-home 4: Add a chart to a dashboard page

**How the workshop helps:** every page follows the same pattern as Top Scorers. Pick inputs, run the query, draw a chart. You'll copy that pattern.

**Starter**

Pick one page whose query is already written (check `sql/`). Then replace its `TODO` comment with a chart:
- **Player Profile:** a line chart of points over time (`px.line`)
- **Standings:** a bar chart of win percentage by team (`px.bar`)

Run `streamlit run app/Home.py` to see it. The page updates when you save the file.

**Done when:** your chart shows up on the page.

**Challenge**

Do one of these:
- On Player Profile, replace the text box with a dropdown of every player (`st.selectbox`)
- Turn your `top_rebounders.sql` from Take-home 2 into its own page by copying `1_Top_Scorers.py`

<details>
<summary>Stuck?</summary>

- Compare your page side by side with `1_Top_Scorers.py`. It has every piece you need.
- Look up chart types in the [Plotly Express gallery](https://plotly.com/python/plotly-express/).
- An error on the page? Read the last line of the red error box first. It usually names the problem.
</details>

---

## Workshop 5: Going live

**In the workshop:** put the dashboard online with Streamlit Community Cloud (free), then brainstorm questions that the group wants answered.

**By the end you will have:**
- A public link to the dashboard that you can share with anyone
- A question of your own to work on

### Take-home 5: Answer a question of your own

You now know every step: SQL, a page, a chart. Pick a sports argument and settle it.

**Starter**

Pick a question from the list below, or invent your own. Then:
1. Write the SQL in a new file in `sql/`
2. Make a new page in `app/pages/` by copying an existing page
3. Open a pull request with a screenshot of your page

**Done when:** your pull request is open.

Question ideas:
- **Home-court advantage:** do teams really win more at home?
- **Head-to-head:** pick two teams and show every game between them
- **Compare two players:** show their stats side by side
- **Close games:** write `sql/close_games.sql` (hints inside) and add a chart

**Challenge**

- **Hot streaks:** find each team's longest winning streak (look up SQL "window functions")
- **Is "clutch" real?** Compare each team's close-game win percentage with its overall win percentage

<details>
<summary>How to deploy (for workshop leads)</summary>

1. Sign in at [streamlit.io/cloud](https://streamlit.io/cloud) with GitHub
2. Click **New app** and choose the repo `data-science-ucsb/sports-stats-explorer`, branch `main`, main file `app/Home.py`
3. The app builds its database automatically the first time it loads
4. Add the live link to the top of the README
</details>

---

## After the workshops

These are bigger group projects for anyone who wants to keep going. You don't need to look at them until the workshops are done.

<details>
<summary>Use real data instead of the fake league</summary>

1. As a group, choose a league. Some options:
   - NBA, using the [`nba_api`](https://github.com/swar/nba_api) Python package
   - Datasets on [Kaggle](https://www.kaggle.com/datasets?search=basketball)
   - Soccer results from [football-data.co.uk](https://www.football-data.co.uk/data.php)
   - Anything else the group cares about
2. Write `scripts/fetch_real_data.py` to download the data and save it as CSV files in the same shape as `data/raw/` (see `data/README.md`)
3. Add useful extra columns to `db/schema.sql`, like three-pointers or fouls
4. Update the tests that assume there are 8 teams
</details>

<details>
<summary>Polish the dashboard</summary>

- Use the same colors on every page
- Add team logos
- Write a better home page that explains what each page answers
</details>

---

## Tips for working together

- **Say what you're working on** in the club channel or on a GitHub issue, so two people don't build the same page.
- **Pull before you start:** `git pull upstream main`. That way you're building on everyone's latest work.
- **Keep pull requests small.** One task per pull request gets reviewed faster.
- **Take-homes are practice.** Leads will merge one working version of each task and give feedback on the rest. Your work counts either way.
- **Ask for help early.** If you've been stuck for 20 minutes, post your error in the channel.

Have an idea that isn't here? Open an issue with the **Task** template, or bring it to the next workshop.
