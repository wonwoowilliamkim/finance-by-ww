# finance-by-ww

> Claude Code-native framework for retail stock research, portfolio
> rebalancing, and forward forecasting.
>
> Claude Code 기반 retail 주식 분석 + portfolio rebalancing + 예측 framework.

---

## What it does / 무엇을 하나

3 main commands, all triggered by natural language:
3가지 메인 명령, 모두 자연어 trigger:

| Trigger | What | Frequency |
|---------|------|-----------|
| `리포트` / `report` | Daily snapshot per holding (cards + summary) | Daily |
| `rebalance` / `포트 진단` | Diversification audit (3-phase) | Monthly / Quarterly |
| `예측` / `outlook` | Multi-horizon forecast (1/3/6/12mo) + 익절 strategy | Quarterly |

Plus auto-fired protocols:
자동 발동:
- `decisions.md` auto-log on every buy/sell/trim
- `pre-mortem` before major new buys (5 failure scenarios)
- Quarterly decision journal review

---

## Why this exists / 왜 만들었나

| Typical retail tools | finance-by-ww |
|----------------------|---------------|
| Static Excel sheets | LLM-native, natural language |
| US English only | Korean + English bilingual (configurable) |
| Simple % stop-loss | Underwater rules, catalyst-based trim, tax-aware |
| No decision tracking | Decision journal + pre-mortem protocol |
| Per-stock signal noise | 3-command architecture (snapshot / structure / future) |

---

## Setup / 설치 (5 min)

1. Clone this repo (or just copy `CLAUDE.md` + `decisions.md`)
2. Place files in your investing project folder
3. Edit `CLAUDE.md` §2 Holdings with your tickers + cost basis
4. (Optional) Install yfinance MCP for live data —
   <https://github.com/Alex2Yang97/yahoo-finance-mcp>
5. Open Claude Code in that folder
6. Type `rebalance` — Phase 1 diagnostic runs

---

## Sample workflow / 사용 예시

```
Morning   → "리포트"                    # daily snapshot
Decision  → (auto-fired pre-mortem before new buy)
Execute   → (auto-fired decisions.md log after buy)
Monthly   → "예측"                      # multi-horizon outlook
Quarterly → "rebalance" + "저널 리뷰"   # structural audit + self-review
```

---

## Disclaimer / 면책

**Not investment advice.** Educational framework only. Past performance
does not predict future returns. You are solely responsible for your
investment decisions.

**투자 조언 아님.** 교육 목적 framework. 과거 성과가 미래 수익을 보장
하지 않음. 모든 투자 결정의 책임은 본인에게.

---

## License

MIT. See [LICENSE](./LICENSE).
