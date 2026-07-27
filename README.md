# projects_db

Shared [json-server](https://github.com/typicode/json-server) database that backs several old React projects
([React_Quiz](https://github.com/Oleg-Irchishyn/React_Quiz), [ReactJS_ToDo_List](https://github.com/Oleg-Irchishyn/ReactJS_ToDo_List))
after their original Heroku + local json-server setup stopped working.

Deployed as a real web service (e.g. on [Render](https://render.com)), not through
my-json-server.typicode.com — that free proxy caps `db.json` at 5 top-level resources and
~10KB, and never persists writes between requests.

## Resources

- `quizQuestions`, `quizForms`, `quizResults` — React_Quiz
- `lists`, `tasks`, `colors` — ReactJS_ToDo_List

## Run locally

```bash
npm install
npm start
```

Serves on `http://localhost:3000` (or `$PORT` if set), e.g. `GET /quizQuestions`, `GET /lists?_embed=tasks`.

## Deploy on Render

1. [dashboard.render.com](https://dashboard.render.com) → **New** → **Web Service** → connect this repo.
2. Runtime: **Node**. Build command: `npm install`. Start command: `npm start`.
3. Free plan is fine — note it spins down after ~15 min idle (cold start ~30-60s on the next request),
   and without a paid persistent disk, any writes (`POST`/`PATCH`/`DELETE`) only survive until the
   service restarts or redeploys, not across those.
4. Deploy, then point the frontend apps' `baseURL` at the resulting `https://<service-name>.onrender.com/`.
