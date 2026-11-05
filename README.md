# crypto-futures-calculators

Plain formulas for USDT-margined perpetual futures. Interactive versions: https://www.liquidityflow.io/tools?utm_source=github&utm_medium=referral&utm_campaign=backlink_github_calculators

Not financial advice. Exchanges use their own maintenance-margin tiers and mark price; always check your exchange's figure.

## 1. Position size from risk
```
qty = (account * risk_pct) / |entry - stop|
notional = qty * entry
leverage_needed = notional / margin
```

## 2. Liquidation price (isolated, simplified, linear USDT perp)
```
long:  liq = entry * (1 - 1/leverage + mmr)
short: liq = entry * (1 + 1/leverage - mmr)
```
mmr = maintenance margin rate. Fees and funding paid from margin move liq closer.

## 3. Trading fees
```
fee = notional * rate   # charged on open AND close
round_trip_taker = 2 * notional * taker_rate
```
Example: 10,000 USDT at 0.06% taker = 6.00 per side, 12.00 round trip.

## 4. Funding cost
```
funding = notional * funding_rate * settlements_held
```
Positive rate: longs pay shorts. Live rates: https://www.liquidityflow.io/funding-rates?utm_source=github&utm_medium=referral&utm_campaign=backlink_github_calculators

## 5. Break-even move
```
breakeven_pct = 2*fee_rate + funding_rate*settlements
```

## License
MIT. Data sources and fee schedules: https://www.liquidityflow.io/fees?utm_source=github&utm_medium=referral&utm_campaign=backlink_github_calculators
