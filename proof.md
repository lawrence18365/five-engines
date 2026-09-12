# Product proof report
_Generated 2026-09-12 10:15 UTC from live data — last 24h_

## Collection health
- collection runs: **1037 total, 964 ok, 55 failed** (93% uptime)
- prices collected: **430,001** across **232** events
- snapshots: **8023** over **1439 minutes** of observation
  - DAZN Bet (altenar): 241 events, 160,528 prices
  - BetMGM (entain): 90 events, 185,424 prices
  - bwin (entain): 14 events, 28,500 prices
  - BetRivers (kambi): 194 events, 118,824 prices
  - NEO.bet (neo): 48 events, 9,049 prices
  - Pinnacle (pinnacle): 162 events, 33,379 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **270**
- exact markets priced by 2 or more engines: **16,609**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,344 | 99.9% |
  | betrivers_on vs bwin | 2,342 | 11.9% |
  | bwin vs neobet | 650 | 10.2% |
  | betmgm vs neobet | 697 | 9.8% |
  | betmgm vs betrivers_on | 7,623 | 9.7% |
  | betrivers_on vs neobet | 766 | 9.3% |
  | dazn_bet vs neobet | 722 | 2.5% |
  | betrivers_on vs pinnacle | 4,041 | 1.9% |
  | betrivers_on vs dazn_bet | 7,442 | 1.7% |
  | bwin vs dazn_bet | 1,962 | 1.6% |
  | betmgm vs dazn_bet | 6,741 | 1.2% |
  | betmgm vs pinnacle | 2,438 | 0.9% |
  | dazn_bet vs pinnacle | 2,718 | 0.9% |
  | bwin vs pinnacle | 776 | 0.5% |
  | neobet vs pinnacle | 308 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,696 | 1.84 | 1,193 | 3,050 |
  | total | 14,006 | 1.89 | 1,154 | 3,440 |
  | team_total | 4,920 | 1.35 | 84 | 898 |
  | moneyline | 992 | 1.80 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — one relationship survives
- observed window: **1439 minutes**, 8038 snapshots
- unbiased (randomised collection order): **2078 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- **survives:** kambi -> altenar (96.8% same direction over 31 moves, p=0.0, ~307s lag)

Note what changed when the contamination was removed: the same pinnacle→entain pair read **78.9% at an 85-second lag** on fixed-order data and reads **65.7% at a 610-second lag** on clean data. Ten minutes is a much less useful window than ninety seconds. The honest version of this feature is materially less exciting than the artifact was.

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | neo → entain | 3 | 100.0% | polling artifact |
  | kambi → altenar | 31 | 96.8% | predictive |
  | pinnacle → kambi | 9 | 77.8% | polling artifact |
  | pinnacle → entain | 44 | 72.7% | polling artifact |
  | entain → pinnacle | 90 | 71.1% | polling artifact |
  | altenar → entain | 326 | 68.1% | polling artifact |
  | pinnacle → altenar | 56 | 67.9% | polling artifact |
  | altenar → pinnacle | 39 | 64.1% | polling artifact |
  | kambi → entain | 10 | 60.0% | polling artifact |
  | entain → altenar | 259 | 59.1% | polling artifact |
  | neo → altenar | 7 | 42.9% | insufficient sample |
  | altenar → neo | 17 | 23.5% | polling artifact |
  | altenar → kambi | 10 | 20.0% | polling artifact |
  | entain → kambi | 48 | 8.3% | polling artifact |
  | entain → neo | 6 | 0.0% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,012**
- passed clean (zero warnings): **79**
- flagged or withheld: **933** (92% of everything found)
- rated high confidence: **36**
- average quoted edge, clean rows: **2.30%**
- average quoted edge, flagged rows: **1.66%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,606**
- best price vs the **median** price: **2.01%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.54%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **67.00** at BetRivers (**+219.0%**)

## Book movement (stale-line detection)
- observed window: **1440 minutes**, 8032 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 13245 | 7456 | 5789 | 43.7% |
  | DAZN Bet | altenar | 12843 | 10141 | 2702 | 21.0% |
  | bwin | entain | 4347 | 3444 | 903 | 20.8% |
  | BetMGM | entain | 12491 | 9929 | 2562 | 20.5% |
  | Pinnacle | pinnacle | 7657 | 6092 | 1565 | 20.4% |
  | NEO.bet | neo | 1168 | 1058 | 110 | 9.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **2,054**
- graded against a closing line so far: **445**
- average CLV: **3.114%** (276 of 445 beat the close)
- average CLV on **clean** rows: **3.429%**
- average CLV on **flagged** rows: **2.989%**

  If the clean rows do not beat the flagged ones over time, our confidence gate is decoration and we would rather know it.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.