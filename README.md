# Crypto Signal Bot Pro — deploy package

A Telegram bot project for crypto market analysis. It includes a working Bitunix public futures Kline adapter, indicators (RSI/MACD/volume/Ichimoku/MA10,20,50,100,150,200), multi-timeframe context, support/resistance, heuristic price-action patterns, breakout/fakeout/liquidity-sweep checks, RSI divergence, confluence scoring, risk levels, RSS news-risk filter, historical backtest command, paper-trade logging, and a TradingView webhook endpoint.

**Important:** This is an advanced starter implementation, not a certified profitable trading system. Price-action/Al Brooks patterns are heuristic approximations. The LBank connector is best-effort and must be validated against your market/account API version. TrueTrade is deliberately disabled until its official API endpoint is confirmed. News RSS matching is a basic risk flag, not a complete event calendar. Live order execution is disabled.

## Deploy on Railway
1. Create a Telegram bot using the official BotFather in Telegram and copy its token privately.
2. Upload this folder to a private GitHub repository.
3. In Railway, create a project → deploy from that GitHub repository. Railway detects the root `Dockerfile`.
4. In the service's **Variables**, set `TELEGRAM_BOT_TOKEN` to your bot token. Leave `ENABLE_LIVE_TRADING=false`.
5. Deploy/redeploy. Open the Telegram bot and send `/start`, then `/signal BTCUSDT 15m`.

Market data for Bitunix public endpoints does not require exchange API keys. Never put tokens in code or send them in chat. For persistent SQLite data, attach a Railway Volume and set `BOT_DB=/data/bot.db`.

## Commands
- `/start` or `/help`
- `/signal BTCUSDT [5m|15m|30m|1h|4h]`
- `/backtest BTCUSDT 15m`
- `/paper BTCUSDT 15m`
- `/coins`
- `/status`

The signal engine requests historical candles at the requested timeframe and adds 1h/4h context where available. `WAIT` is a valid result; do not treat confidence as a probability of profit.
