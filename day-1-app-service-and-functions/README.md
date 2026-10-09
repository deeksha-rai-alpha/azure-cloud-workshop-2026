# Day 1 - App Service and Azure Functions

A plain HTML page hosted on **Azure App Service** that calls three **Azure Functions**. Workshop material; the code is small by design.

| Part | Path | Trigger / type | What it does |
|---|---|---|---|
| Web page | `webapp/index.html` | Static HTML + JavaScript `fetch` | Shows a version badge, calls `/api/hello` and `/api/students` |
| `hello` | `functions/hello` | HTTP (GET, POST), anonymous | Returns a JSON greeting for `?name=`; uses optional `GREETING` app setting |
| `heartbeat` | `functions/heartbeat` | Timer, every 5 minutes (`0 */5 * * * *`) | Writes an "alive" log line |
| `students` | `functions/students` | HTTP + **Azure SQL input binding** | Returns rows of `dbo.Students` as JSON |
| SQL | `students.sql` | T-SQL | Creates and seeds `dbo.Students` |

## Setup

1. Create the table by running `students.sql` in the Azure SQL **Query editor** (connected to the same database as your connection string).
2. Create a Function App (the workshop used Consumption plan, Windows, Node.js with the portal code editor) and add the functions by pasting each `index.js` / `function.json`. Compare `functions/_reference/host.json` with the app's `host.json` (extension bundle `[4.*, 5.0.0)`).
3. App settings: `SqlConnectionString` (required for `students`), `GREETING` (optional).
4. CORS: allow `https://portal.azure.com` and your Web App URL (no trailing slash).
5. Edit `webapp/index.html`: replace `Your Name`, and set `FUNCTION_BASE_URL` to `https://<your-function-app-default-domain>/api`.
6. Deploy the page: see `DEPLOY_COMMANDS.txt` (ZIP deploy with `az webapp deploy`). The trainers' original notes are in `WORKSHOP_NOTES.txt`.

**Local running:** the page can be opened in a browser, but it needs a deployed Function App to return anything. There is no local Functions setup in this folder.
