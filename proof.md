# Product proof report
_Generated 2026-09-11 00:02 UTC from live data — last 24h_

## Collection health
- collection runs: **173 total, 170 ok, 2 failed** (98% uptime)
- prices collected: **59,959** across **94** events
- snapshots: **453** over **105 minutes** of observation
  - DAZN Bet (altenar): 62 events, 15,621 prices
  - BetMGM (entain): 17 events, 23,270 prices
  - BetRivers (kambi): 53 events, 16,398 prices
  - NEO.bet (neo): 30 events, 2,059 prices
  - Pinnacle (pinnacle): 18 events, 2,611 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **222**
- exact markets priced by 2 or more engines: **3,895**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 674 | 12.2% |
  | betmgm vs betrivers_on | 2,559 | 10.9% |
  | betrivers_on vs neobet | 740 | 8.2% |
  | betmgm vs dazn_bet | 1,725 | 2.6% |
  | betrivers_on vs dazn_bet | 1,778 | 2.0% |
  | dazn_bet vs neobet | 498 | 1.8% |
  | betrivers_on vs pinnacle | 850 | 1.5% |
  | betmgm vs pinnacle | 832 | 1.1% |
  | dazn_bet vs pinnacle | 706 | 0.6% |
  | neobet vs pinnacle | 280 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,624 | 1.83 | 376 | 544 |
  | spread | 3,396 | 2.04 | 580 | 603 |
  | team_total | 2,642 | 1.25 | 18 | 310 |
  | moneyline | 176 | 2.06 | 30 | 64 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines
- observed window: **105 minutes**, 456 snapshots
- no relationship yet clears the sample and significance bar
- relationships tested: 18, rejected as noise or insufficient sample: 10

  Scored on whether the follower moves the SAME DIRECTION, against a 50% baseline with an exact binomial test, and requiring at least 20 paired moves. Counting who moved first would have given the opposite answer: Altenar reprices far more often than Kambi and a naive count credited it with 87% of all leads, but when Altenar moved first Kambi followed the same way only 40% of the time.

  **Caveat:** lead/lag is NOT published yet: every snapshot so far was collected in a FIXED book order, which makes whichever book is polled first appear to lead the others by exactly the polling gap. Collection order was randomised 23 minutes ago; results become publishable after 60 minutes of unbiased data..

## What the gate rejected
- opportunities detected: **347**
- passed clean (zero warnings): **75**
- flagged or withheld: **272** (78% of everything found)
- rated high confidence: **39**
- average quoted edge, clean rows: **1.00%**
- average quoted edge, flagged rows: **3.93%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines: **2,000**
- median improvement from taking the best price: **4.9%**
- largest: **Under 9.50** — 1.54 worst vs **3.10** at BetMGM (**+101.3%**)

## Book movement (stale-line detection)
- observed window: **105 minutes**, 454 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 1206 | 408 | 798 | 66.2% |
  | Pinnacle | pinnacle | 622 | 335 | 287 | 46.1% |
  | NEO.bet | neo | 332 | 189 | 143 | 43.1% |
  | BetMGM | entain | 1599 | 977 | 622 | 38.9% |
  | DAZN Bet | altenar | 1002 | 688 | 314 | 31.3% |

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.