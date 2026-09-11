# Product proof report
_Generated 2026-09-11 20:03 UTC from live data — last 24h_

## Collection health
- collection runs: **1642 total, 1424 ok, 212 failed** (87% uptime)
- prices collected: **316,019** across **255** events
- snapshots: **5224** over **1306 minutes** of observation
  - DAZN Bet (altenar): 235 events, 92,480 prices
  - BetMGM (entain): 84 events, 109,364 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 72,206 prices
  - NEO.bet (neo): 43 events, 5,092 prices
  - Pinnacle (pinnacle): 89 events, 17,347 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **256**
- exact markets priced by 2 or more engines: **13,900**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 100.0% |
  | betrivers_on vs bwin | 2,326 | 11.5% |
  | bwin vs neobet | 635 | 10.7% |
  | betmgm vs betrivers_on | 7,428 | 10.5% |
  | betmgm vs neobet | 685 | 10.2% |
  | betrivers_on vs neobet | 750 | 9.2% |
  | bwin vs dazn_bet | 1,862 | 2.2% |
  | betmgm vs dazn_bet | 6,057 | 1.7% |
  | dazn_bet vs neobet | 706 | 1.6% |
  | betrivers_on vs dazn_bet | 6,760 | 1.4% |
  | betrivers_on vs pinnacle | 3,106 | 1.4% |
  | bwin vs pinnacle | 766 | 0.8% |
  | betmgm vs pinnacle | 2,364 | 0.8% |
  | dazn_bet vs pinnacle | 2,138 | 0.7% |
  | neobet vs pinnacle | 292 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 12,963 | 1.86 | 1,147 | 2,710 |
  | total | 12,587 | 1.83 | 1,116 | 2,399 |
  | team_total | 4,236 | 1.34 | 70 | 656 |
  | moneyline | 934 | 1.80 | 114 | 365 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1308 minutes**, 5230 snapshots
- unbiased (randomised collection order): **1226 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 21 | 100.0% | polling artifact |
  | kambi → neo | 53 | 94.3% | polling artifact |
  | neo → entain | 77 | 87.0% | polling artifact |
  | kambi → altenar | 163 | 76.7% | noise |
  | entain → pinnacle | 353 | 75.1% | polling artifact |
  | altenar → neo | 101 | 70.3% | polling artifact |
  | neo → pinnacle | 13 | 69.2% | polling artifact |
  | entain → neo | 63 | 63.5% | weak |
  | entain → altenar | 599 | 59.6% | polling artifact |
  | altenar → pinnacle | 152 | 59.2% | polling artifact |
  | pinnacle → kambi | 315 | 57.8% | polling artifact |
  | entain → kambi | 332 | 57.5% | polling artifact |
  | kambi → pinnacle | 571 | 57.3% | polling artifact |
  | pinnacle → altenar | 70 | 57.1% | noise |
  | pinnacle → entain | 289 | 57.1% | polling artifact |
  | neo → kambi | 58 | 56.9% | polling artifact |
  | kambi → entain | 195 | 55.4% | polling artifact |
  | altenar → entain | 421 | 52.5% | polling artifact |
  | altenar → kambi | 145 | 52.4% | polling artifact |
  | neo → altenar | 39 | 46.2% | noise |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,083**
- passed clean (zero warnings): **163**
- flagged or withheld: **920** (85% of everything found)
- rated high confidence: **26**
- average quoted edge, clean rows: **1.27%**
- average quoted edge, flagged rows: **2.70%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,625**
- best price vs the **median** price: **2.03%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.73%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Utah State ** — 11.00 worst vs **20.00** at BetRivers (**+81.8%**)

## Book movement (stale-line detection)
- observed window: **1306 minutes**, 5225 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 7146 | 4775 | 2371 | 33.2% |
  | DAZN Bet | altenar | 5907 | 3999 | 1908 | 32.3% |
  | BetMGM | entain | 7200 | 4875 | 2325 | 32.3% |
  | bwin | entain | 4191 | 2979 | 1212 | 28.9% |
  | Pinnacle | pinnacle | 3803 | 2739 | 1064 | 28.0% |
  | NEO.bet | neo | 1269 | 1084 | 185 | 14.6% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,593**
- graded against a closing line so far: **10**
- average CLV: **3.919%** (6 of 10 beat the close)
- average CLV on **clean** rows: **-1.728%**
- average CLV on **flagged** rows: **6.339%**

  If the clean rows do not beat the flagged ones over time, our confidence gate is decoration and we would rather know it.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.