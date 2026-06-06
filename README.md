# Stock Analyzer

A lightweight Python toolkit for A-share market analysis, technical-indicator research, signal scanning, and alert monitoring.

This project is designed for developers, retail investors, and quantitative-learning users who want a readable and extensible codebase for studying Chinese A-share market data. It supports real-time and historical data analysis, configurable indicators, custom trading signals, active scanning, and email-based notifications.

> **Disclaimer**  
> This project is for research, learning, and engineering experimentation only. It does not provide financial advice, investment recommendations, or trading guarantees. Use it at your own risk.

---

## Features

- Real-time and historical A-share data analysis
- Configurable stock universe and monitoring targets
- Custom technical indicators and signal rules
- Active signal scanning across selected stocks
- Real-time signal monitoring
- Email notification support for detected signals
- Multi-process monitoring mode
- Built-in examples of practical indicators:
  - MACD
  - HalfTrend
  - Smart Money Concepts / SMC
  - NMACD
  - SSL Channel
- Built-in examples of trading signals:
  - HHC
  - MACD + RSI
  - MA + NMACD + RSI

---

## Project Status

This repository is currently in an early maintenance stage.

The current focus is to make the project easier to install, understand, extend, and contribute to.

Planned improvements include:

- Cleaner English documentation
- Safer configuration examples
- Better dependency management
- Unit tests for indicators and signal logic
- More modular data-source adapters
- More examples for custom indicators and custom signal strategies
- Better contributor guidelines

---

## Repository Structure

The main source code is located under the `stock-analyser` directory.

Key modules include:

- `exchange`  
  Data access and market-data retrieval.

- `analysis`  
  Technical-analysis logic.

- `indicator`  
  Custom technical indicators.

- `trading_signals`  
  Signal definitions. A signal can be based on a single indicator or a combination of indicators.

- `notifiers`  
  Notification logic. The current implementation supports email alerts and can be extended to other channels such as webhooks, Discord, Telegram, Slack, or other messaging services.

- `config`  
  Runtime configuration, including monitored stocks, signal selection, scanning settings, and notifier settings.

---

## Requirements

- Python 3.6 or above

Common dependencies include:

- `pandas`
- `numpy`
- `tushare`
- `matplotlib`

Install dependencies with:

```bash
pip install -r requestment.txt
```

> Note: the dependency file name is currently kept as `requestment.txt` to match the existing repository. It may be renamed to `requirements.txt` in a future cleanup.

---

## Configuration

The main runtime configuration is defined in `config.json`.

Typical configuration sections include:

### `pairlists`

The list of A-share symbols to monitor.

Supported formats include:

```text
sh000001
000001.XSHG
```

### `signals`

The available trading-signal definitions.

### `scan`

The signal rules enabled for active scanning or real-time monitoring.

### `notifier`

Email-notification settings, including:

- sender email address
- SMTP server
- SMTP port
- email username
- email password or app-specific password

> **Security note**  
> Do not commit real email credentials, API tokens, or app-specific passwords to the repository. Use a local config file, environment variables, or a secret manager whenever possible.

---

## Usage

### 1. Single-process real-time monitoring

Run:

```bash
python main.py
```

This starts real-time monitoring and sends email notifications when configured signal conditions are met.

### 2. Multi-process real-time monitoring

Run:

```bash
python multi_mode_main.py
```

This enables multi-process monitoring for a larger stock universe or heavier signal workloads.

### 3. Active signal scanning

Run or customize:

```bash
python scan_signals.py
```

Use `scanner.scan_pairs` to configure:

- target stock list
- trading signal
- analysis period or time window

The scanner returns signal-related data. In the existing convention:

- `is_hot = True` indicates a potential buy signal
- `is_cold = True` indicates a potential sell signal
- other returned fields contain signal-specific diagnostic data

---

## Extending the Project

You can extend the project in several ways.

### Add a new indicator

Create or update an indicator module under the indicator-related code path, then expose the result to the trading-signal layer.

### Add a new trading signal

Create a new signal rule in the `trading_signals` module. A signal can use one indicator or combine multiple indicators.

### Add a new notification channel

Extend the `notifiers` module. The current project supports email notifications, but the structure can be expanded to support webhook-based services or messaging platforms.

### Replace or add a data source

The data-source layer is currently based on an A-share data wrapper. It can be adapted to support other data providers if the returned market-data format is normalized for the analysis layer.

---

## Roadmap

Planned maintenance work:

- [ ] Rewrite setup instructions in a clearer format
- [ ] Add `config.example.json`
- [ ] Remove hard-coded local or sensitive configuration assumptions
- [ ] Rename `requestment.txt` to `requirements.txt`
- [ ] Add tests for core indicators
- [ ] Add tests for trading-signal outputs
- [ ] Add sample scanner workflows
- [ ] Improve error handling for data-source failures
- [ ] Improve email-notifier safety and documentation
- [ ] Add contributor guidelines

---

## Contributing

Issues and pull requests are welcome.

Good first contributions include:

- fixing documentation gaps
- adding installation notes
- improving configuration examples
- adding unit tests
- adding new indicators
- adding new signal examples
- improving error handling
- adding new notification backends

Before submitting a pull request, please make sure the change is clearly scoped and includes enough explanation for review.

---

## Fork Attribution

This repository is a maintained fork of the original `chentaiyi/stock-analyzer` project.

Original author information from the upstream README:

- Author: chentaiyi
- WeChat: 501745
- Email: 501745@qq.com

This fork is maintained by Li Zhou / `zhouliion` with the goal of improving documentation, maintainability, testing, and extensibility for open-source A-share analysis and monitoring use cases.

---

## License

This project is released under the MIT License.
