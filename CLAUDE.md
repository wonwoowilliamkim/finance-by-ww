# CLAUDE.md — finance-by-ww

> Claude Code-native framework for retail stock research.
> Fork this, fill in §2 Holdings, start typing triggers.
>
> 한국+영어 혼합 default. §3 Tone & Language Rules에서 변경 가능.

## 1. Mode

**QUICK-HIT.** No plan-first, no verify-loop, no Phase ceremony.
This is a hobby retail-investing framework — just deliver. If you also
run an academic/research stream in Claude Code, keep that in a separate
folder with its own CLAUDE.md.

## 1.5. 3대 명령 (Architecture)

이 folder의 모든 분석은 3개 주요 명령으로 구성:

| 명령 | Trigger | 주기 | 목적 | 출력 |
|------|---------|------|------|------|
| **리포트** | "리포트" / "오늘 어때" / "[ticker] 어떻게" | 매일 (옵션) | 오늘 무슨 일 — snapshot | §3 daily card |
| **rebalance** | "rebalance" / "포트 진단" | 월/분기 | 구조적 결함 진단 + diversification | §9 3-phase (diagnostic→long-list→deep dive) |
| **예측** | "예측" / "outlook" / "전망" | 분기 (또는 큰 변동 후) | 미래 + 익절 strategy | §12 multi-horizon + 익절 rule |

이 3개는 각각 다른 시야:
- **리포트** = 현재 (오늘)
- **rebalance** = 구조 (portfolio 전체 형태)
- **예측** = 미래 (1-12개월 시나리오)

세 가지 모두 §3 daily card aesthetic 공유 (한 줄 진단 → 의미 → 표 → risk → Action/Verdict).

추가 보조 명령:
- §10 decisions.md auto-log (모든 buy/sell/trim 결정 후)
- §11 pre-mortem (큰 신규 매수 전 자동)
- "저널 리뷰" (분기 self-correction)

## 2. Current Holdings (update when positions change)

> **Replace this template with your own holdings.** Real Cluster column
> uses §9's mapping rules; confirm cluster when adding new tickers.

| Ticker | Company | Shares | Entry | Position | GICS | Real Cluster |
|--------|---------|--------|-------|----------|------|--------------|
| TICKER1 | Company Name 1 | X shares | $XX (avg) | ~$X,XXX | GICS Sector | Real Cluster |
| TICKER2 | Company Name 2 | X shares | $XX (avg) | ~$X,XXX | GICS Sector | Real Cluster |
| TICKER3 | Company Name 3 | X shares | $XX | ~$X,XXX | GICS Sector | Real Cluster |

새 종목 추가 시 Real Cluster는 user confirm 필수.
Multi-lot 진입 시 blended avg 표시, 세부 lot별 가격/날짜는 decisions.md.

**Total invested: ~$XX,XXX**

Real cluster breakdown (cost basis):
- Cluster A: $X,XXX (~XX%)
- Cluster B: $X,XXX (~XX%)
- ...

## 3. Default Report Format — "1순위 조합" (C + B 하이브리드)

When I ask for a daily/event report, follow this structure exactly.

### Tone & Language Rules
- **Verbs / adjectives**: English OK (Hold / Cut / Trim / rally / dropped /
  crushed / clean / shaky / alarming).
- **Nouns / concepts**: Korean preferred (갈림길, 발판, 천장, 진공,
  꼭대기 정리, 거래량, 잔치, 손님 등).
- **Tone**: 약간 재밌게 (잔치/손님/짐 싸다 같은 메타포 OK), 단 시시콜콜하지 않게.
  Baseline is neutral analyst, salt with one or two figures of speech per card.
- **No financial advice disclaimers.** This is personal research notes.

> If you want a different language mix (English-only, Korean-only,
> Japanese, etc.), edit this section. The downstream sections reference
> "한 줄 진단" / "의미" labels — change those too if you swap languages.

### Structure (top to bottom)

````
# [Date] 종목 리포트

## 용어 미니사전 (한 번만 — 이미 익숙하면 첫 보고서 이후 생략)
[short bullet list explaining 이동평균선 / RSI / 거래량 / 천장 / 발판 /
Distribution top in plain Korean]

---

## [Date] 오늘의 액션
| 종목 | Action | Stop | First trim |
| TICKER1 | ... |
| TICKER2 | ... |
| TICKER3 | ... |

---

## WHY — 한 단락
[2-3 sentences: what happened today, two scenarios (a)/(b), which
signal supports which, then short cost-basis read across all holdings.]

---

## 카드 (보유 종목별)

### 🟡/🔴/🟢 [TICKER] — [Company]
```
현가: $X   오늘: ±X%
진입가: $X   →   ±X% (~±$X)
```
**한 줄 진단**: [pithy 1-sentence, with metaphor OK]
**의미**: [volume / MA / momentum reading in plain language]

| | 가격 | 의미 |
| 반드시 지켜야 함 | $X | ... |
| Add zone | $X | ... |
| First trim | $X | ... |
| Second trim / 다음 발판 | $X | ... |

**Scenarios (6-month)**:
- 🟢 Bull (XX%): $XXX — [trigger 조건 한 줄]
- 🟡 Base (XX%): $XXX — [한 줄]
- 🔴 Bear (XX%): $XXX — [한 줄]
- **Expected value**: $XXX (확률 가중) vs 현가 $XXX → ±X%
- **R/R**: upside $X / downside $X = X.X : 1
  - 2.0:1 미만 → 비효율, skip 또는 size down
  - 2.0:1 이상 → 무난
  - 3.0:1 이상 → 적극 add 고려

확률 합 100%. Trigger 조건은 명확한 사건 (어닝, 발사, 매크로 지표). 막연한
"rally"/"crash" X.

**가장 큰 risk**: [1-2 sentences]
**Action**: **Hold/Cut/Trim**. Stop $X. [conditional logic if relevant]

---

## 한 줄 종합
[Portfolio-wide takeaway — sector themes, what single level/event
decides multiple names' fate. Note which cluster moves together,
which names are independent risk legs.]
````

### Color emoji per ticker
- 🟢 strongest / cleanest setup
- 🟡 caution / mixed
- 🔴 weakest / underwater

### Card-card consistency
All cards must have the SAME structure (현가/진입가 → 한 줄 진단 →
의미 → table → risk → Action). 차이를 비교하기 쉽게.

## 4. Mini-Dictionary (used in reports, not need re-explained)

- **이동평균선** — 최근 N일 종가 평균. 위에 있으면 bullish, 밑이면
  bearish. 자주 발판 역할.
  - 20일 = 최근 한 달
  - 50일 = 최근 두 달 반
  - 200일 = 1년치 장기 추세선
- **RSI (0~100)** — 달리는 속도 점수. 70+ overheated, 30- oversold,
  50 = neutral.
- **거래량** — 그날 손바뀜한 주식 수. 가격 움직임에 의미를 부여하는 변수.
- **천장 (resistance)** — 위로 막히는 가격대.
- **발판 (support)** — 밑에서 받쳐주는 가격대.
- **Distribution top (꼭대기 정리)** — 신고가에 비정상적 거래량 동반.
  큰 손 짐 싸는 신호.
- **진공** — 발판 사이 빈 구간. 한 번 깨지면 다음 발판까지 빠르게 빠짐.
- **갭다운** — 자고 일어났더니 어제 종가보다 한참 밑에서 시작. 어닝/뉴스 후 흔함.
  Stop-loss 룰 안 통함 (잠든 사이 이미 그 가격).
- **Forward P/E** — 앞으로 1년 예상 이익 대비 주가. 12 이하 cheap, 25+ expensive.
- **FCF (Free Cash Flow)** — 영업으로 만든 진짜 현금. + 흑자, − 적자. Utility/성장 capex 크면 - 정상.
- **Dividend yield** — 주가 대비 1년 배당. 2-3% 평범, 3-5% high-yield, 5%+ 의심 (배당컷 risk).
- **Capex** — 사업 확장에 쓴 돈. 많으면 FCF 깎임.
- **Defensive** — 시장 빠질 때 덜 빠지는 성격 (β < 0.8 영역).
- **Cyclical** — 경기 따라 출렁이는 성격 (β > 1.0).
- **Secular growth** — 경기와 무관하게 장기 성장. AI/healthcare aging/energy transition 등.

## 5. Data Sources

- **yfinance MCP** (`.mcp.json`) — quick single-ticker queries in chat
  (현재 price, market cap, basic financials, MA, RSI, volume).
  - Server: <https://github.com/Alex2Yang97/yahoo-finance-mcp>
- **Local yfinance** (`pip install yfinance` 또는 `uv pip install yfinance`)
  — heavy/batch computation 용. Rebalance (§9)의 correlation matrix / beta /
  stress는 6+ 종목 × 6개월 일별 데이터 + numpy 계산이라 MCP보다 로컬 스크립트가
  안정적. 또한 subagent는 MCP 못 봄 (§6 #4) → 배치 계산은 항상 local.
- **WebSearch** — quarterly results, news, catalysts.
- **IR pages / SEC EDGAR** — runway, guidance, 10-Q numbers.

> Setup note: rebalance/forecast 같은 무거운 계산 전 `pip install yfinance numpy pandas`
> 확인. 없으면 Claude가 설치 후 진행.

## 6. Red Lines (project-specific)

1. **No speculation.** "Data not available" > guessing. 진짜 돈 걸린
   결정이라 hallucination = 실제 손실.
2. **Cite source for every number** — yfinance / filing URL / news link.
3. **No knowledge-cutoff fallback.** If MCP/WebSearch fails for a
   specific number, say so explicitly.
4. **Subagent ≠ MCP access** (known Claude Code limitation). If
   delegating to market-researcher agent, pre-fetch data in main
   session and paste into the agent prompt as ground truth.
5. **Stop when done.** No "anything else?" — wait for next ask.

## 7. Useful Slash Commands (from local-scope plugins)

`/earnings`, `/dcf`, `/comps`, `/sector`, `/screen`, `/thesis`,
`/morning-note`, `/catalysts` — Anthropic financial-services
plugins, Investor-scope only.

## 8. Trigger Phrases (so I don't have to spell the format out)

- "리포트" / "오늘 어때" / "[ticker] 어떻게 됐어" → use the full
  3-card format above
- "한 줄로" / "quick read" → just the 오늘의 액션 table + 한 줄 종합
- "deep dive [ticker]" → full card + extra paragraph on chart structure
  and longer-term thesis check
- "용어 다시" → re-include mini-dictionary at top
- "rebalance" / "포트 진단" / "diversification check" → §9 Rebalance
  Protocol 3-phase 실행 (Phase 1만 즉시, 2/3는 confirm 후)
- (자동) buy/sell/trim/hold 결정 → §10 decisions.md 자동 log
- "저널 리뷰" / "decision journal review" → §10 quarterly review
- "pre-mortem [ticker]" / "악마의 옹호인" → §11 pre-mortem
- "예측" / "outlook" / "전망" / "익절 plan" → §12 multi-horizon full (전 종목)
- "예측 [ticker]" / "[ticker] outlook" / "익절 [ticker]" → §12 variant single-stock

## 9. Rebalance / Diversification Protocol

"rebalance" trigger 시 3-phase 진행. Phase 사이마다 STOP.

### Phase 1 — Portfolio Diagnostic

§2 holdings 전부 읽어 다음 9개 분석:

1. **Sector exposure (dual view)** — 다음 2개 표 동시 출력:

   (a) **GICS 명목 분류** — yfinance sector field 그대로 (참고용)

   | Sector | USD | % |

   (b) **Real cluster (수동 매핑)** — 사업/risk 실체 기반

   | Real Cluster | 매핑 룰 (예시 — your tickers will differ) |
   |--------------|---------|
   | Space | 위성 통신/제조/발사 — ASTS, PL, RKLB |
   | Defense | 방산 — LMT, RTX, GD, NOC |
   | Energy | 화석/신재생/utility 외 — OXY, XOM, CVX |
   | Industrials (real) | 농기계/기계/물류 — DE, CAT, UNP |
   | Healthcare | 제약/의료/생명과학 — UNH, JNJ, LLY |
   | Software/AI | 클라우드/AI/사이버 — MSFT, GOOG, PLTR, CRWD |
   | Hardware/Semi | 반도체/장비 — NVDA, TSM, AMD, ASML |
   | Consumer Staples | 필수소비재 — PG, KO, COST |
   | Consumer Disc | 자율 소비재 — AMZN, TSLA, NKE |
   | Financials | 은행/보험/결제 — JPM, V, MA |
   | Utilities | 전력/물 — NEE, AEP, SO |
   | Real Estate | REIT — O, PLD |
   | Materials | 금속/화학 — FCX, LIN |
   | Communication | 통신/미디어 — VZ, T, META |

   ⚠ **GICS vs Real cluster discrepancy 자동 체크**:
   각 종목 GICS vs Real cluster 비교, 다르면 한 줄씩 명시.
   예: "PL: GICS 'Industrials' → Real 'Space' (위성 EO)"

   ⚠ **Cluster concentration warning**:
   - 단일 cluster ≥ 50% → "concentrated"
   - 단일 cluster ≥ 70% → "highly concentrated"

   ⚠ **새 종목 add 시**:
   §2에 새 ticker 추가될 때마다 Real cluster 매핑 confirm 요청.

2. **Size factor** — yfinance market cap 받아 position-weighted avg.
   분포 (small <$2B / mid $2-10B / large $10-200B / mega >$200B).

3. **Style factor** — P/E, P/S, FCF 부호 기반 growth/value 판정.
   Weighted growth-tilt 점수 (-1 deep value ~ +1 pure growth).

4. **Correlation matrix** — 6-month daily return NxN.
   yfinance daily returns → pandas로 직접 계산. "추정" X. 0.6+ cluster
   강조.

5. **Cost-basis health** — 종목별 현가 vs entry. USD + %. -20% 이상
   underwater면 ⚠ 표시.

6. **Capital efficiency 경고** — 큰 underwater (-25% 이상) 종목에
   "redeploy 고려" 옵션 명시. 결정은 user.

7. **Beta (market sensitivity)** — yfinance에서 종목별 beta 받아
   position-weighted portfolio beta 계산. 의미: "S&P 500 1% 하락 시
   포트폴리오 약 X% 하락 (이론값)".
   - Beta < 0.7: defensive
   - 0.7~1.3: market-like
   - 1.3 이상: aggressive

8. **Stress scenario (Real cluster 기준)** — 다음 simultaneous 충격
   가정한 portfolio drawdown 시뮬:
   - Space: -30%
   - Energy: -20%
   - Industrials (real): -15%
   - Healthcare/Staples/Utilities: -10%
   - Software/AI: -25%
   - Hardware/Semi: -25%
   - 기타: -20%

   계산: position-weighted 손실 합 → portfolio USD 손실 + %.
   "2022 growth crash 같은 상황 시 대략 이 수준 빠짐"이라고 해석.

9. **Position-sized risk on stops** — §3 카드의 각 종목 stop 가격 트리거
   가정 시 종목별 손실 + portfolio % impact. 합산 = "모든 stop 동시
   트리거되면 portfolio -X%".

### Phase 1 Output Format (§3 daily report aesthetic)

```
# Portfolio Diagnostic ([날짜])

## Portfolio Snapshot
| 종목 | Real Cluster | Position | P/L % | β | Note |
|------|--------------|----------|-------|---|------|
| TICKER1 | Cluster | $X | +X% | X.XX | |
| ...

## WHY — 한 단락
[3-4 줄 narrative. 오늘 진단의 핵심을 자연어로. "이 portfolio는 X에 베팅하는
1-factor 노출, 갈림길은 (a)/(b)..." 같은 daily report 스타일.]

**Cost-basis 읽기**:
- 종목별 P/L USD 한 줄씩
- 포트폴리오 총 unrealized: $X (X%)
- 가장 큰 단일 risk 한 줄

---

## 진단 카드 (factor별, 5장)

### 🚨 1. Sector Concentration (real cluster 기준)
**한 줄 진단**: [GICS vs Real cluster 어긋남 + concentration 정도 한 줄]
**의미**: [왜 GICS table이 misleading한지, 진짜 cluster %는 얼마인지]

| Real Cluster | USD | % |
| ClusterA | $X | X% |
| ... |

GICS discrepancy: [있으면 한 줄씩, 없으면 "없음"]
**가장 큰 risk**: [단일 cluster 충격 시 portfolio 영향]
**시사점**: [다음 add 방향 한 줄]

---

### 🟡 2. Size + Style
**한 줄 진단**: [size 분포 + style tilt 한 줄]
**의미**: [growth-tilt 점수의 실질 의미]

- Weighted avg market cap: $X B
- 분포: large X% / mid X% / small X%
- Weighted growth-tilt: +X.X (-1 deep value ~ +1 pure growth)
- 종목별: TICKER1 +1.0 / TICKER2 +0.95 / ...

**가장 큰 risk**: [growth crash 시나리오 한 줄]
**시사점**: [value/balanced 보강 필요 여부]

---

### 🔴 3. Correlation Cluster
**한 줄 진단**: [high-corr 쌍 한 줄 — "사실상 한 종목" 같은 비유]
**의미**: [공통 risk factor 한 단락]

         T1     T2     T3     T4     T5
T1       1.00   ...
...

High-cluster (≥0.6): [쌍 + 비유]
Independent legs: [어떤 종목들이 진짜 분산]

**가장 큰 risk**: [corr cluster 깨질 때 시나리오]
**시사점**: [cluster를 합산 risk budget으로 보라는 한 줄]

---

### 🚨 4. Beta + Stress Drawdown
**한 줄 진단**: [β 분류 + stress -X% 한 줄]
**의미**: [시장 충격 시나리오를 평이한 말로]

| | 값 | 의미 |
| Portfolio β | X.XX | 시장 -1% → 너 -X.X% |
| -10% 시나리오 | -X.X% | 흔한 조정 |
| -20% 시나리오 | -X.X% | 정상 bear market |
| Stress (cluster shock) | -X.X% | 2022 growth crash식 |

종목별 β contribution: [짧게]

**가장 큰 risk**: [감당 가능성 self-test 질문 한 줄]
**시사점**: [defensive 필요 여부 한 줄]

---

### 🟢 5. Cost-basis Health + Stop Discipline
**한 줄 진단**: [평가손익 상태 + stop 규율 한 줄]
**의미**: [현재 손실 + 손절 트리거 시 누적 시나리오]

| 종목 | P/L | Stop hit 시 추가 손실 | Portfolio % impact |
| ... |

- 현재 평가손: -$X (-X%)
- 모든 stop 동시 hit 시 추가: -$X (-X%)
- **누적 worst case (현재 + stops)**: -X%

Underwater 종목 (-20%+): [⚠ ticker — capital efficiency 한 줄]

**가장 큰 risk**: [stop 안 지킬 위험 — 감정적 hold]
**시사점**: [재배치 검토 옵션 한 줄]

---

## Identified gaps (한 단락)
[비어있는 factor 자연어 정리 — 다음 Phase 2의 방향성]

---

## 한 줄 종합
[Daily report 종합처럼: 진단의 핵심 하나 + 가장 중요한 다음 행동 한 줄]
```

→ STOP after Phase 1. user confirm 후 Phase 2.

### Phase 2 — Candidate Long-list (5-7개)

Phase 1 결과 기반 비어있는 factor 채우는 후보.

Hard constraints:
- US-listed (NYSE/Nasdaq) — adjust for your market
- Market cap $1B – $500B
- Liquid (avg daily volume > $50M)
- 자본: $1,500 – $3,000 per name (adjust to your portfolio size)
- 최종 추천 2-3개 (over-fragmentation 방지)

Soft preferences:
- 비어있는 sector 우선
- 기존 종목과 6M 상관계수 < 0.4 예상
- 최소 1개 dividend payer + FCF positive
- 최소 1개 macro hedge (utility, healthcare, defensive)
- Beta가 너무 높으면 → low-beta (<0.8) 후보 우선
- Stress drawdown 너무 크면 → defensive 비중 우선
- Anti-recency: 단순 hot 종목 (모두가 아는 mega-cap) 제외

Process:
1. WebSearch "current year sector rotation" / "factor leadership" /
   "under-loved sectors healthy FCF" 3개+ source
2. 각 sector 1-2개 candidate
3. yfinance로 valuation + beta + 차트 확인
4. 아래 Phase 2 Output Format으로 출력

### Phase 2 Output Format (§3 daily report aesthetic)

```
# Phase 2 — Candidate Long-list ([날짜])

## Market Context — 한 단락
[3-4 줄 narrative. Sector rotation / factor leadership / under-loved
영역. Source 3개+ WebSearch 기반.]

## 후보 요약 table
| Ticker | Real Cluster | Verdict | β 변화 | Redeploy 후보? | 한 줄 |
|--------|--------------|---------|--------|----------------|-------|
| ... |

---

## Candidate 카드 (5-7장)

### 🟢⚡ [TICKER] — [Company]

현가: $X        시총: $XB
β: X.XX ([defensive/market-like/aggressive])
배당: X.X% | FCF +/-$XB | Forward P/E X

**한 줄 진단**: [왜 이 종목 후보로 올라왔는가 — 비유 OK]
**의미**: [회사 사업 한 줄 + 현재 valuation/timing 한 줄]

| | 값 | 의미 |
| Fills gap | [cluster/factor] | [한 줄] |
| Portfolio β 변화 | X.XX → X.XX | Δ ±X.XX |
| 기존 corr 예상 | X.X | [낮음/중간/높음] |
| Entry timing | [Good/OK/Bad] | [근거 한 줄] |

**가장 큰 risk**: [한 줄 — 명확한 사건/원인]
**Verdict**: [🟢 best fit / 🟡 OK fit / ⚡ redeploy 후보 / 🔴 skip — 이유 한 줄]

---

(5-7개 카드 동일 구조)
```

Emoji 규칙:
- 🟢 best fit (β 효과 큼 + entry timing 좋음 + 갭 정확)
- 🟡 OK fit (한두 가지 약점)
- ⚡ redeploy 후보 (existing underwater 종목 갈아치우기 후보)
- 🔴 skip (timing/valuation 나쁨)

```
## 2-pick combo preview
[조합별 portfolio β 효과 table — 어떤 조합이 가장 균형 잡힌지]

| 조합 | New β | Δ | Cluster 추가 |
| ... |

## 한 줄 종합
[내가 골라야 한다면 + 이유 1-2줄. user가 자유롭게 결정 가능하게.]
```

→ STOP after Phase 2. user의 final 2-3 pick → Phase 3.

### Phase 3 — Card 분석 (선택 종목 deep dive)

§3 카드 format 사용. 진입가 미정이라 다음 조정:

- "진입가" → "Proposed entry zone $X–X"
- 추가 줄: "**Position size 권장**: $X,XXX (포트 X%)"
- 추가 줄: "**Fills gap**: [어떤 factor 채우는지 한 줄]"
- 추가 줄: "**Beta**: X.XX → 추가 시 portfolio beta가 X에서 X로"
- 추가 줄: "**Stress 영향**: 추가 후 stress drawdown -X.X% → -X.X%로
  [개선/악화/중립]"
- Bull/Bear scenarios + R/R ratio §3 그대로
- Action 줄 명시 형식: "**Action**: Buy zone $X–X / Stop $X / First trim $X / 또는 Skip + 사유"

자동 trigger:
- 매수 결정 → §11 pre-mortem 자동 발동 (1년 -50% 시나리오)
- 매수 실행 → §10 decisions.md 자동 log

나머지 (한 줄 진단 / 의미 / 가격 table / risk) 동일.

### Rules

1. Correlation, beta, stress 모두 직접 계산. 추정 X.
2. Subagent 위임 X — main session 처리.
3. Phase 사이마다 STOP.
4. Underwater 종목 별도 "redeploy 고려" 옵션 (결정은 user).
5. No speculation. yfinance / SEC / dated source.
6. Phase 1의 9개 항목 다 채워야 함. 누락 시 "데이터 없음" 명시.
7. **Computation discipline (생성 코드 sanity check)** — rebalance 계산
   코드는 매 실행 fresh 생성되므로, 다음 검증 통과 후에만 결과 신뢰:
   - **Beta**: cov/var ddof 통일 — `np.cov` 기본 ddof=1, `np.var` 기본 ddof=0
     불일치 주의. 반드시 같은 ddof 사용 (`np.var(market, ddof=1)`).
   - **Beta cross-check**: 계산 beta를 yfinance beta와 비교 — 10배 이상
     차이나면 코드 의심.
   - **Correlation matrix**: 대각선 = 1.0 확인 (아니면 정렬 버그).
   - **Weights**: 합 = 1.0 (±0.01) 확인.
   - **Beta None-guard**: yfinance `beta`가 None일 수 있음 → fallback (1.0)
     + 사용 시 명시.
   - **재실행 안정성**: 숫자가 wildly 다르면 fetch 실패/NaN 처리 의심.
   - **원칙**: LLM 생성 분석 코드는 검증 없이 믿지 말 것. 1회 sanity check
     필수.

## 10. Decision Journal

모든 portfolio 결정 (buy/sell/trim/add/hold-with-conviction) 즉시
`./decisions.md`에 entry 추가.

### File: `./decisions.md` (relative to this CLAUDE.md)

### Entry format
| Date | Ticker | Action | Size | Price | Why | Outcome target | Re-eval |

예 (generic): | YYYY-MM-DD | TICKER | Hold | X shares | $XX | thesis 한 줄 | $YY+ | YYYY-MM-DD |

### Auto-log triggers
- 신규 매수
- 부분/전체 매도
- Trim
- 명시적 "Hold with conviction"
- Stop 트리거 cut

### Quarterly review (3/31, 6/30, 9/30, 12/31 또는 "저널 리뷰")
1. 지난 분기 모든 entry 읽기
2. Outcome target vs 실제 결과 비교
3. 정확도 % + 평균 winner/loser ratio
4. 잘한 결정 1-2개 + 잘못한 결정 1-2개 pattern
5. "다음 분기 self-correction" 한 단락

### Why
Retail 알파의 대부분 = 자기 결정 패턴 인지+교정. Journal 없으면 같은 실수 반복.

## 11. Pre-mortem Protocol

큰 결정 직전 "1년 뒤 -50% 가정" 시나리오 → thesis 약점 강제 노출.

### 자동 발동 조건
- 신규 종목 매수
- 기존 포지션 +50% 이상 add
- Underwater 포지션 redeploy
- 전체 portfolio 30%+ 차지 단일 position

### User 명시 trigger
- "pre-mortem [ticker]" / "이거 사기 전에 점검" / "악마의 옹호인"

### Format

```
## Pre-mortem — [TICKER] (가정: 1년 뒤 -50%)

### 실패 시나리오 5개
1. [시나리오] — [확률 X%] — [무엇이 일어났는가]
2. ...

### Mitigation
| # | 사전 방지 가능 | 어떻게 | 지금 액션 |

### Re-decision
- 유지 / 변경 / Skip + 이유
```

### Why
Kahneman: 두뇌는 "왜 실패했는가" (과거형)는 잘 답하지만 "실패 가능성"
(미래형)은 못 답함. Pre-mortem이 미래를 과거로 reframe.

## 12. Multi-horizon Forecast + 익절 Strategy

"예측" / "outlook" / "전망" / "익절 plan" trigger 시 실행.
§3 daily report card aesthetic 유지 — Forecast table이 가격 levels table 대체.

### Output format (template)

````
# Multi-horizon Forecast ([date])

## Confidence disclaimer (한 단락)
각 horizon별 신뢰도 명시:
- **1mo**: medium (technical + 임박 catalyst)
- **3mo**: medium-low (단기 어닝 cycle)
- **6mo**: low (catalyst window 누적)
- **12mo**: storytelling (secular thesis 검증용, 가격 X)

→ 결과 paste 받는 사람이 신뢰도 misread 안 하게 명시.

## Per-ticker 카드 (§3 daily card 변형)

### [emoji] [TICKER] — [Company]
```
현가: $X    오늘: ±X%
진입가: $X    →    ±X% (~±$X)
```

**Forecast table**:
| Horizon | Bull (%) | Base (%) | Bear (%) | Expected | vs 진입가 |
|---------|----------|----------|----------|----------|-----------|
| 1mo  | $X (XX%) | $X (XX%) | $X (XX%) | $X | +X% |
| 3mo  | $X (XX%) | $X (XX%) | $X (XX%) | $X | +X% |
| 6mo  | $X (XX%) | $X (XX%) | $X (XX%) | $X | +X% |
| 12mo | $X (XX%) | $X (XX%) | $X (XX%) | $X | +X% |

(확률 합 100% per row. Trigger 조건은 명확한 사건 기반.)

**Key driver at each horizon**:
- 1mo: [핵심 catalyst 한 줄]
- 3mo: ...
- 6mo: ...
- 12mo: ...

**익절 Strategy** (cost basis 기반):
- **+X% 시**: 1차 trim (1/3 또는 1/2 — 어느 쪽이고 왜)
- **+Y% 시**: 2차 trim
- **+Z% 시**: 3차 또는 풀 익절 or let it ride
- **Trailing stop**: peak에서 -X% 빠지면 자동 cut
- **종목 특유 rule**: [어닝 hold? Catalyst 후 일괄? Underwater 본전 회복 시?]

**Cost-basis 고려 한 줄**: [현재 +/-X% 상황에서 trim 우선순위 변화]
**가장 큰 risk (12mo)**: [한 줄]
**Recommendation**: [Hold / partial trim / add / cut signal — 이유 한 줄]

---

(전 종목 동일 구조)

## Portfolio-level 익절 Framework
(아래 6개 종합 rule)
````

### Portfolio-level Framework rules

1. **Underwater 종목**: 본전 회복 ≠ trim signal. 본전 +5% 도달 시
   진짜 익절 zone 시작. 예외: catalyst 직후 즉시 1/3 trim
2. **승자 동시 winning** (high-corr cluster): 단일 종목 portfolio
   30%+ 차지 시 자동 1/3 trim, cluster 70% 초과 시 즉시 trim
3. **분기 rebalance** (3/31, 6/30, 9/30, 12/31): 단일 종목 30%+
   자동 trim, 단일 cluster 60%+ 시 다음 add는 다른 cluster
4. **Catalyst 직후 자동 trim**: 발사 성공/어닝 beat/M&A 루머 후
   1-3일 안 1/3 trim (binary 해제 = profit lock 의무)
5. **Portfolio total target**: 누적 +20% 시 universal 10% trim,
   +40% 시 추가 10% trim, -15% 시 손실 종목 cut 검토
6. **세금** (adapt to your jurisdiction):
   - **Korea resident, US stocks**: 양도소득 연 250만원 공제. 익절
     시점 분산, 12월 후반 익절 자제 → 1월로 미루기 (다음 해 공제)
   - **US resident, US stocks**: 1년 미만 short-term capital gains
     (ordinary income tax), 1년+ long-term (낮은 rate). 가능하면
     매수 후 1년+ 보유 후 익절
   - **기타 jurisdictions**: 본인 세법에 맞게 trim timing 조정

### Rules

1. 모든 가격/확률 yfinance + dated news + 최근 어닝 기반. Speculation X.
2. 6mo/12mo는 "high uncertainty" 명시.
3. 익절 % 추천 시 cost basis 명확히 인용.
4. 방금 매수 종목은 1mo 평타, 3mo부터 의미 있는 시나리오.
5. Deep underwater 종목은 "익절" 대신 "본전 회복선" + "redeploy trigger" 논의.
6. Stop after report. 추가 행동 권유 X.

### Variant — Single-stock

"예측 [TICKER]" / "[TICKER] outlook" / "익절 [TICKER]" trigger 시:
- 해당 ticker 카드 1장만 출력
- Portfolio framework skip
- Confidence disclaimer 1줄로 축약

### Auto-fired contexts (선택적, user 명시 확인)

- 분기 끝 (3/31, 6/30, 9/30, 12/31) → 전체 portfolio 예측 재갱신 제안
- 단일 종목 ±20% 이상 변동 → 해당 ticker single-stock 예측 갱신 제안
- 새 종목 add 후 1주일 → 해당 ticker 첫 예측 생성 제안
