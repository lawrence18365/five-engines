# Product proof report
_Generated 2026-09-12 08:55 UTC from live data — last 24h_

## Collection health
- collection runs: **1119 total, 1023 ok, 78 failed** (91% uptime)
- prices collected: **426,463** across **232** events
- snapshots: **8022** over **1438 minutes** of observation
  - DAZN Bet (altenar): 241 events, 158,257 prices
  - BetMGM (entain): 86 events, 181,364 prices
  - bwin (entain): 14 events, 28,500 prices
  - BetRivers (kambi): 194 events, 117,002 prices
  - NEO.bet (neo): 48 events, 8,602 prices
  - Pinnacle (pinnacle): 162 events, 32,689 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **268**
- exact markets priced by 2 or more engines: **16,453**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,344 | 99.9% |
  | betrivers_on vs bwin | 2,342 | 11.9% |
  | bwin vs neobet | 648 | 10.0% |
  | betmgm vs betrivers_on | 7,611 | 9.8% |
  | betmgm vs neobet | 695 | 9.6% |
  | betrivers_on vs neobet | 764 | 8.6% |
  | dazn_bet vs neobet | 720 | 2.1% |
  | bwin vs dazn_bet | 1,962 | 2.0% |
  | betrivers_on vs pinnacle | 4,037 | 1.9% |
  | betrivers_on vs dazn_bet | 7,398 | 1.7% |
  | betmgm vs dazn_bet | 6,733 | 1.3% |
  | dazn_bet vs pinnacle | 2,716 | 1.0% |
  | betmgm vs pinnacle | 2,430 | 0.9% |
  | bwin vs pinnacle | 776 | 0.5% |
  | neobet vs pinnacle | 306 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,644 | 1.85 | 1,193 | 3,016 |
  | total | 13,956 | 1.89 | 1,146 | 3,384 |
  | team_total | 4,878 | 1.36 | 84 | 902 |
  | moneyline | 992 | 1.80 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1436 minutes**, 8013 snapshots
- unbiased (randomised collection order): **1997 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → neo | 20 | 100.0% | polling artifact |
  | entain → pinnacle | 56 | 92.9% | polling artifact |
  | kambi → pinnacle | 38 | 92.1% | polling artifact |
  | pinnacle → neo | 21 | 85.7% | polling artifact |
  | neo → kambi | 39 | 82.1% | polling artifact |
  | neo → entain | 28 | 78.6% | polling artifact |
  | pinnacle → entain | 91 | 71.4% | polling artifact |
  | entain → kambi | 45 | 71.1% | polling artifact |
  | pinnacle → altenar | 45 | 68.9% | polling artifact |
  | entain → neo | 47 | 68.1% | polling artifact |
  | altenar → neo | 73 | 64.4% | polling artifact |
  | entain → altenar | 522 | 60.5% | polling artifact |
  | neo → altenar | 15 | 60.0% | polling artifact |
  | altenar → kambi | 55 | 58.2% | polling artifact |
  | altenar → entain | 475 | 57.5% | polling artifact |
  | neo → pinnacle | 7 | 57.1% | polling artifact |
  | altenar → pinnacle | 77 | 55.8% | polling artifact |
  | kambi → altenar | 56 | 53.6% | noise |
  | pinnacle → kambi | 33 | 42.4% | polling artifact |
  | kambi → entain | 26 | 42.3% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,044**
- passed clean (zero warnings): **93**
- flagged or withheld: **951** (91% of everything found)
- rated high confidence: **3**
- average quoted edge, clean rows: **2.15%**
- average quoted edge, flagged rows: **1.48%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **4,562**
- best price vs the **median** price: **1.77%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.29%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **67.00** at BetRivers (**+219.0%**)

## Book movement (stale-line detection)
- observed window: **1439 minutes**, 8023 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 13105 | 7311 | 5794 | 44.2% |
  | DAZN Bet | altenar | 12721 | 10003 | 2718 | 21.4% |
  | Pinnacle | pinnacle | 7576 | 5954 | 1622 | 21.4% |
  | BetMGM | entain | 12412 | 9836 | 2576 | 20.8% |
  | bwin | entain | 4327 | 3444 | 883 | 20.4% |
  | NEO.bet | neo | 1144 | 997 | 147 | 12.8% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **2,024**
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