Predict the Cup

A single-page, no-backend World Cup score prediction game. Pick scores for a Round of 32 slate, get scored against a Poisson-model "house bot," save your total to a local leaderboard, and challenge a friend via a shareable link.

Live logic only — no server, no database, no real-time data. Everything runs client-side in index.html.

What it actually does
Renders a fixed set of 6 Round of 32 matches (hardcoded in the script, not fetched from any API).
Lets you enter a predicted score for each match.
Compares your picks against a frozen, illustrative results set baked into the code — these are placeholder outcomes for demo purposes, not live or confirmed tournament results.
Generates a "house bot" prediction per match using a Poisson model based on static attack/defense ratings for each team.
Scores both you and the bot: 5 points for an exact scoreline, 2 for correct match outcome (win/draw/loss), 0 otherwise.
Saves your score to a leaderboard stored in the browser's localStorage — this data is local to your browser only, not shared or synced anywhere.
Lets you generate a challenge link (your name + score encoded in the URL hash) to send to a friend. Opening that link lets them see your score as a target — there's no server relaying this, it's just data riding in the URL.
How the bot's prediction works

Each team has a static { attack, defense } rating (average goals scored/conceded), used to compute expected goals (λ) for each side in a matchup:

homeλ = homeAttack × (awayDefense / leagueAverage)
awayλ = awayAttack × (homeDefense / leagueAverage)

Those λ values feed into a Poisson probability mass function to estimate win/draw/loss chances, and the rounded λ values become the bot's predicted scoreline.

This is a deliberately simple model — no home advantage, no current form, no injuries, no recency weighting — and the sample size behind the team ratings is small. Treat the odds as a toy, not a forecast.

Running it

No build step, no dependencies, no install.

Clone or download this repo.
Open index.html directly in a browser.

That's it. It's a static file.

Data sources & attribution
Fixtures: openfootball/worldcup.json (CC0)
Team strength ratings: computed via the same method used in the code (average goals for/against), sourced from martj42/international_results (CC0)
Match "results" used for scoring are an illustrative/frozen dataset for gameplay purposes — not live tournament data
Limitations (be aware before relying on any of this)
The results used to score your picks are not real, confirmed match outcomes — they're a static demo dataset.
The bot's team ratings are hand-set/approximated for a limited set of teams; unlisted teams fall back to a league-average rating.
The leaderboard is per-browser (localStorage), not global or persistent across devices.
The "challenge a friend" feature has no backend — it only works by manually sharing the generated link.
Disclaimer

Independent learning/side project. Not affiliated with or endorsed by FIFA, SAP, or the DFB.
