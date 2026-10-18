# Boundary Cricket Score Centre — Website

A responsive website with a match list, scorecard, batting/bowling tabs, run rate, overs, wickets, striker indicators when the provider supplies them, and a clearly labelled demo mode.

## Requirements
- Node.js 18 or later
- A cricket data API account/token for real scores

## Run locally
1. Extract this project ZIP.
2. Open a terminal in the project folder.
3. Run `npm install`.
4. Copy `.env.example` to `.env`.
5. Run `npm start`.
6. Open `http://localhost:3000`.

By default `DEMO_MODE=true`. This shows invented illustrative examples only; these are not live match scores.

## Configure a live Cricket API
The starter server uses a CricketLiveApi-style API shape as an example:
- `GET /api/v1/cricket/matches/live`
- `GET /api/v1/cricket/scorecard/{matchId}`
- Bearer token in the `Authorization` header

The provider docs currently describe those patterns at https://cricketliveapi.com/cricket-api. Provider availability, pricing, current endpoint details, coverage, and returned JSON fields must be verified with your provider before use.

1. Sign up with the API provider and select a plan that covers live scores and full scorecards.
2. Copy your API token from its dashboard.
3. Set `.env` like this:
   ```env
   DEMO_MODE=false
   PORT=3000
   CRICKET_API_TOKEN=put_your_real_token_here
   CRICKET_API_BASE=https://cricketliveapi.com/api/v1/cricket
   ```
4. Restart with `npm start`.
5. If your provider uses different routes or response fields, update the two API routes in `server.js` and the field adapters in `public/index.html` to match the provider's official docs.

**Security:** Never put a secret API token in browser JavaScript. This project keeps the token on the Node server and the browser calls your own `/api/...` routes. Do not commit `.env` to a public repository.

## Included features
- Responsive match list and match filters
- Demo/live status indicator
- Scorecard, batting, and bowling views
- Batter runs, balls, fours, sixes, strike rate where supplied
- Bowler overs, maidens, runs, wickets, economy where supplied
- Team score, innings, wickets, overs, run rate where supplied
- Auto-refresh every 30 seconds in API mode
- API errors displayed in the UI

## Notes
- The website is read-only for API scores. Manual scoring is not enabled in this API version.
- Provider APIs differ. The adapter is intentionally small and may need field mapping for the chosen provider.
- A provider may not explicitly flag striker/non-striker. Boundary displays those markers only when the response identifies them, rather than guessing.
