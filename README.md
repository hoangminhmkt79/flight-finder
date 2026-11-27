# Flight Finder

A small GitHub Actions workflow that searches for the cheapest one-way flight to Bangkok and sends the results to a Telegram topic.

## Run the Bangkok fare search

1. Open [Actions](../../actions/workflows/bangkok-flex.yml).
2. Select **Run workflow**.
3. Enter the center departure date in `YYYY-MM-DD` format. The default is `2027-02-08`.
4. Select **Run workflow** again.

The workflow checks the center date plus or minus one day, compares SGN and CXR departures, and includes both BKK and DMK. It returns each origin/date option as a separate fare, sorted by price, then sends the report to Telegram. It searches for one adult and one-way travel. Checked baggage and extra fees are not verified.

A run uses up to six SerpApi searches (three dates × two origins). Commits do not trigger searches.

## Required GitHub Actions secrets

In **Settings → Secrets and variables → Actions**, add:

- `SERPAPI_API_KEY`
- `TELEGRAM_BOT_TOKEN`
- `TELEGRAM_CHAT_ID`
- `TELEGRAM_THREAD_ID`

Use the chat and topic that contain `@MM_suggest_travel_bot`. The workflow checks the bot username and confirms Telegram accepted the message in the expected chat and topic. Never commit secret values to this repository.

## Workflow source

[`bangkok-flex.yml`](.github/workflows/bangkok-flex.yml)
